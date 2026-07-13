# 17. Database Operations

## `DbContext` in Background Service

As covered in the Dependency Injection section, `DbContext` is **Scoped** by default and must never be injected directly into a `BackgroundService` (a Singleton). Always resolve it through a fresh `IServiceScope` per unit of work.

```csharp
public class DataSyncWorker : BackgroundService
{
    private readonly IServiceScopeFactory _scopeFactory;

    public DataSyncWorker(IServiceScopeFactory scopeFactory) => _scopeFactory = scopeFactory;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        using var timer = new PeriodicTimer(TimeSpan.FromMinutes(5));
        while (await timer.WaitForNextTickAsync(stoppingToken))
        {
            using var scope = _scopeFactory.CreateScope();
            var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();

            var pending = await db.SyncItems
                .Where(x => !x.Synced)
                .Take(500)
                .ToListAsync(stoppingToken);

            foreach (var item in pending) item.Synced = true;
            await db.SaveChangesAsync(stoppingToken);
        }
    }
}
```

## Transactions

Use explicit transactions when multiple related changes must succeed or fail together.

```csharp
using var scope = _scopeFactory.CreateScope();
var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();

using var transaction = await db.Database.BeginTransactionAsync(stoppingToken);
try
{
    db.Orders.Update(order);
    db.Ledger.Add(ledgerEntry);
    await db.SaveChangesAsync(stoppingToken);
    await transaction.CommitAsync(stoppingToken);
}
catch
{
    await transaction.RollbackAsync(stoppingToken);
    throw;
}
```

In many cases, EF Core wraps a single `SaveChangesAsync()` call in an implicit transaction automatically — explicit transactions matter most when you need multiple `SaveChangesAsync` calls, or mix EF Core changes with raw SQL, to be atomic together.

## Bulk Insert / Bulk Update

EF Core's default `SaveChangesAsync()` issues one round-trip per changed entity (batched somewhat by the provider, but still relatively inefficient for thousands of rows). For genuinely large batch operations common in background processing (e.g., importing 100,000 records from a file), consider:

- **EF Core's `ExecuteUpdate`/`ExecuteDelete`** (EF Core 7+) for set-based updates without loading entities into memory:
```csharp
await db.Orders
    .Where(o => o.Status == "Pending" && o.CreatedAt < cutoff)
    .ExecuteUpdateAsync(s => s.SetProperty(o => o.Status, "Expired"), stoppingToken);
```
- **Third-party bulk libraries** (e.g., EFCore.BulkExtensions) for true SQL bulk-insert/bulk-update performance when inserting/updating tens of thousands of rows at once.
- **Raw `SqlBulkCopy`** (SQL Server-specific) for maximum-throughput bulk inserts straight from a `DataTable`.
- **Batching** — process records in chunks (e.g., 500–1000 at a time), calling `SaveChangesAsync` per chunk rather than accumulating one giant change set, to keep memory and transaction log usage manageable.

```csharp
const int batchSize = 500;
foreach (var chunk in records.Chunk(batchSize))
{
    db.AddRange(chunk);
    await db.SaveChangesAsync(stoppingToken);
    db.ChangeTracker.Clear(); // avoid change tracker bloat across batches
}
```

## Retry Logic

Background services often run unattended for long periods — transient DB failures (network blips, deadlocks, connection pool exhaustion, Azure SQL throttling) should not crash the whole service.

### EF Core's Built-In Connection Resiliency
```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(connectionString, sqlOptions =>
        sqlOptions.EnableRetryOnFailure(
            maxRetryCount: 5,
            maxRetryDelay: TimeSpan.FromSeconds(10),
            errorNumbersToAdd: null)));
```
This automatically retries transient failures (as classified by the provider) for individual operations.

### Application-Level Retry (e.g., with Polly — see Resilience Patterns section)
```csharp
var retryPolicy = Policy
    .Handle<DbUpdateException>()
    .WaitAndRetryAsync(3, attempt => TimeSpan.FromSeconds(Math.Pow(2, attempt)));

await retryPolicy.ExecuteAsync(async () =>
{
    await db.SaveChangesAsync(stoppingToken);
});
```

## Connection Pooling

ADO.NET / EF Core providers pool physical database connections automatically by default — opening/closing a `DbContext` doesn't necessarily open/close a real network connection each time; it borrows from a pool keyed by connection string.

### Why It Matters for Background Services
- Creating a **new scope per unit of work** (as recommended) is cheap precisely *because* connection pooling avoids the cost of establishing a fresh physical connection every time.
- **Connection pool exhaustion** can occur if you run many concurrent background operations (e.g., parallel `Task.WhenAll` over hundreds of items, each opening its own scope/DbContext) without bounding concurrency — tune `Max Pool Size` in the connection string and/or use `SemaphoreSlim` to cap concurrent DB operations (see Advanced Concurrency section).
- Always **dispose** your `DbContext`/scope (`using`) promptly so connections are returned to the pool quickly rather than held longer than necessary.

```
Server=.;Database=AppDb;Max Pool Size=100;Min Pool Size=5;Connection Timeout=30;
```

## Practical Checklist for DB Work in Background Services
1. New scope per unit of work — never hold a `DbContext` across the service's whole lifetime.
2. Pass `stoppingToken` into every async EF Core call.
3. Batch large operations; clear the change tracker between batches.
4. Wrap multi-step changes in explicit transactions when atomicity is required.
5. Enable connection retry-on-failure for transient resiliency.
6. Bound concurrency to avoid exhausting the connection pool.
7. Log row counts and durations for each DB operation batch — essential for diagnosing slow nightly jobs later.