# Database in .NET Background Service (Worker Service)

---

# What is a Background Service?

A **Background Service** is a service that runs continuously in the background after the application starts.

It does **not** wait for an HTTP request.

Common uses:

- Send Emails
- Process Queue
- Generate Reports
- Database Cleanup
- Scheduled Jobs
- File Processing
- Background Synchronization
- Notification Service

---

# Register Worker

```csharp
builder.Services.AddHostedService<Worker>();
```

### Why?

Registers the Worker with Dependency Injection.

The Worker starts automatically when the application starts.

---

# BackgroundService Lifetime

`BackgroundService` is registered as a **Singleton**.

This means only **one Worker object** exists.

```
Application Starts

↓

Worker Created

↓

ExecuteAsync()

↓

Runs Continuously

↓

Application Stops

↓

Worker Disposed
```

---

# Why Singleton?

A background task should run only once.

Example:

Email Sender

Correct

```
One Worker

↓

Send Emails
```

Wrong

```
Five Workers

↓

Same Email Sent Five Times
```

---

# Service Lifetimes

| Lifetime | Created | Destroyed |
|-----------|----------|-----------|
| Singleton | Once | Application Stops |
| Scoped | One per Scope | Scope Ends |
| Transient | Every Request | After Use |

---

# Web API vs Background Service

## ASP.NET Core Web API

```
HTTP Request

↓

Create Scope

↓

Controller

↓

DbContext

↓

Response

↓

Dispose Scope
```

ASP.NET Core automatically creates the scope.

---

## Background Service

```
Application Starts

↓

Worker

↓

No HTTP Request

↓

No Scope
```

There is no automatic scope.

You must create one manually.

---

# Why DbContext is Scoped?

`DbContext` is **not thread-safe**.

Every request or operation should use a fresh `DbContext`.

Correct

```
Request 1

↓

DbContext 1

-------------------

Request 2

↓

DbContext 2
```

Wrong

```
Request 1

↓

Same DbContext

↓

Request 2

↓

Same DbContext
```

Problems

- Thread conflicts
- Wrong tracking
- Memory growth
- Connection issues

---

# Why Can't Singleton Use Scoped?

```
Worker

↓

Singleton

(Application Lifetime)

-------------------------

DbContext

↓

Scoped

(Short Lifetime)
```

A Singleton lives much longer than a Scoped service.

Therefore,

❌ Do not inject `DbContext` directly into `BackgroundService`.

---

# Solution

Create a temporary scope.

```
Worker

↓

Create Scope

↓

Create DbContext

↓

Use Database

↓

Dispose Scope
```

---

# Register DbContext

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")));
```

### Why?

- Registers DbContext
- Configures SQL Server
- Enables Dependency Injection

---

# Inject IServiceScopeFactory

```csharp
public class Worker(
    IServiceScopeFactory scopeFactory)
    : BackgroundService
{
}
```

### Why?

Creates a new DI Scope whenever the Worker needs a Scoped service.

---

# Create Scope

```csharp
using var scope = scopeFactory.CreateScope();
```

### Why?

Creates a temporary scope.

Inside this scope you can safely use:

- DbContext
- Repository
- Other Scoped services

---

# Why using?

```csharp
using var scope = scopeFactory.CreateScope();
```

Automatically disposes the scope.

Equivalent to

```csharp
var scope = scopeFactory.CreateScope();

try
{
}
finally
{
    scope.Dispose();
}
```

`using` is shorter and recommended.

---

# IServiceProvider

```csharp
scope.ServiceProvider
```

### Why?

Gets services from the current scope.

Examples

- DbContext
- Repository
- Logger
- HttpClient
- Custom Services

---

# GetRequiredService()

```csharp
var context =
    scope.ServiceProvider
         .GetRequiredService<AppDbContext>();
```

### Why?

Gets a required service.

If not registered,

```
Throws Exception
```

Recommended.

---

# GetService()

```csharp
var context =
    scope.ServiceProvider
         .GetService<AppDbContext>();
```

Returns

```
DbContext

or

null
```

Used when a service is optional.

---

# Difference

| GetService() | GetRequiredService() |
|--------------|----------------------|
| Returns null | Throws Exception |
| Optional | Required |
| Less common | Recommended |

---

# DbContext

Main EF Core class.

Responsible for

- Reading data
- Inserting data
- Updating data
- Deleting data

Example

```csharp
public class AppDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }
}
```

---

# Read All Data

```csharp
var employees =
    await context.Employees
        .ToListAsync(stoppingToken);
```

Reads all records.

---

# Read One Record

```csharp
var employee =
    await context.Employees
        .FirstOrDefaultAsync(
            e => e.Id == id,
            stoppingToken);
```

Returns the first matching record.

Returns `null` if no record exists.

---

# Find by Primary Key

```csharp
var employee =
    await context.Employees
        .FindAsync(new object[] { id }, stoppingToken);
```

Searches by Primary Key.

---

# Check Record Exists

```csharp
bool exists =
    await context.Employees
        .AnyAsync(
            e => e.Id == id,
            stoppingToken);
```

Returns

- true
- false

---

# Count Records

```csharp
int total =
    await context.Employees
        .CountAsync(stoppingToken);
```

Returns total records.

---

# Insert Data

```csharp
await context.Employees
    .AddAsync(employee, stoppingToken);

await context
    .SaveChangesAsync(stoppingToken);
```

Adds a new record.

---

# Insert Multiple Records

```csharp
await context.Employees
    .AddRangeAsync(
        employees,
        stoppingToken);

await context
    .SaveChangesAsync(stoppingToken);
```

---

# Update Data

```csharp
context.Employees.Update(employee);

await context
    .SaveChangesAsync(stoppingToken);
```

`Update()` only marks the entity as modified.

Database changes happen in `SaveChangesAsync()`.

---

# Delete Data

```csharp
context.Employees.Remove(employee);

await context
    .SaveChangesAsync(stoppingToken);
```

`Remove()` marks the entity for deletion.

Deletion happens when `SaveChangesAsync()` is called.

---

# SaveChangesAsync()

```csharp
await context
    .SaveChangesAsync(stoppingToken);
```

Writes all pending changes to the database.

Without this,

```
Nothing is saved.
```

---

# Async Methods

Common async methods

```csharp
ToListAsync()

FirstOrDefaultAsync()

SingleOrDefaultAsync()

AnyAsync()

CountAsync()

FindAsync()

AddAsync()

AddRangeAsync()

SaveChangesAsync()
```

Advantages

- Better performance
- Doesn't block thread
- Recommended

---

# CancellationToken

```csharp
CancellationToken stoppingToken
```

Represents a cancellation request.

---

# Why Pass CancellationToken?

If the application stops,

```
Application Stops

↓

Cancellation Requested

↓

Database Operation Stops

↓

Worker Exits Gracefully
```

Always pass it to async EF Core methods.

---

# AsNoTracking()

```csharp
var employees =
    await context.Employees
        .AsNoTracking()
        .ToListAsync(stoppingToken);
```

Use for read-only data.

Benefits

- Faster
- Less memory
- Better performance

---

# Tracking

```
Database

↓

DbContext

↓

Track Changes

↓

SaveChangesAsync()
```

Use when

- Update
- Delete

---

# No Tracking

```
Database

↓

Read

↓

No Tracking
```

Use when

- Reports
- Dashboard
- Lists
- Read-only APIs

---

# Complete Flow

```
Application Starts

↓

Worker Created

↓

Loop Starts

↓

Create Scope

↓

ServiceProvider

↓

GetRequiredService()

↓

DbContext

↓

Read / Insert / Update / Delete

↓

SaveChangesAsync()

↓

Dispose Scope

↓

Wait

↓

Repeat
```

---

# Worker vs Web API

| Worker Service | Web API |
|----------------|---------|
| Singleton | Scoped |
| No HTTP Request | HTTP Request |
| No Automatic Scope | Automatic Scope |
| CreateScope() Required | CreateScope() Not Required |
| Uses IServiceScopeFactory | Inject DbContext Directly |

---

# Best Practices

✅ Register `DbContext` with `AddDbContext()`

✅ Never inject `DbContext` directly into `BackgroundService`

✅ Always create a new scope

✅ Use `using var scope`

✅ Use `GetRequiredService()`

✅ Pass `CancellationToken`

✅ Use async EF Core methods

✅ Use `AsNoTracking()` for read-only queries

✅ Always call `SaveChangesAsync()`

✅ Dispose the scope automatically with `using`

---

# Common Interview Questions

- What is `BackgroundService`?
- Why is `BackgroundService` Singleton?
- Why is `DbContext` Scoped?
- Why can't Singleton use Scoped?
- Why use `IServiceScopeFactory`?
- What does `CreateScope()` do?
- Difference between `GetService()` and `GetRequiredService()`?
- Why use `CancellationToken`?
- Why use `AsNoTracking()`?
- Why use `SaveChangesAsync()`?
- Why use async EF Core methods?
- Why create one `DbContext` per scope?
- Why doesn't Web API require `CreateScope()`?
- Why is `using var scope` recommended?



------------



# Why Can't BackgroundService Use DbContext Directly?

`BackgroundService` is registered as a **Singleton**.

```csharp
builder.Services.AddHostedService<Worker>();
```

`DbContext` is registered as **Scoped**.

```csharp
builder.Services.AddDbContext<AppDbContext>();
```

So,

```text
BackgroundService = Singleton

DbContext = Scoped
```

A **Singleton cannot directly use a Scoped service**.

If you try,

```csharp
public class Worker(
    AppDbContext context)
    : BackgroundService
{
}
```

The application throws an exception.

```text
Cannot consume scoped service
'AppDbContext'
from singleton
'Worker'.
```

Why?

Because the Worker lives for the **entire application**.

The `DbContext` should live only for **one scope**.

---

# Solution

Create a **new Scope** whenever the Worker needs `DbContext`.

```text
Worker

↓

Create Scope

↓

Create DbContext

↓

Use Database

↓

Dispose Scope
```

---

# IServiceScopeFactory

`IServiceScopeFactory` creates a **new Dependency Injection (DI) Scope**.

Inject it into the Worker.

```csharp
public class Worker(
    IServiceScopeFactory scopeFactory)
    : BackgroundService
{
}
```

Create a scope.

```csharp
using var scope = scopeFactory.CreateScope();
```

Get `DbContext`.

```csharp
var context = scope.ServiceProvider
    .GetRequiredService<AppDbContext>();
```

Flow

```text
Worker

↓

IServiceScopeFactory

↓

CreateScope()

↓

Scope

↓

DbContext

↓

Database
```

### Why use it?

- Creates a temporary scope
- Allows using Scoped services
- Automatically disposed with `using`

---

# IServiceProvider

`IServiceProvider` is the **Dependency Injection container**.

It stores all registered services.

Examples:

- DbContext
- Repository
- Logger
- HttpClient

Inject it.

```csharp
public class Worker(
    IServiceProvider serviceProvider)
    : BackgroundService
{
}
```

Create a scope.

```csharp
using var scope = serviceProvider.CreateScope();
```

Get `DbContext`.

```csharp
var context = scope.ServiceProvider
    .GetRequiredService<AppDbContext>();
```

Flow

```text
Worker

↓

IServiceProvider

↓

CreateScope()

↓

Scope

↓

DbContext

↓

Database
```

---

# IServiceScopeFactory vs IServiceProvider

| IServiceScopeFactory | IServiceProvider |
|----------------------|------------------|
| Creates scopes | Provides registered services |
| Call `CreateScope()` | Can also call `CreateScope()` |
| Focused on creating scopes | General DI container |
| Used mainly for scopes | Used to resolve any service |

---

# Which One Should You Use?

Both are correct.

### Option 1 (Recommended)

```csharp
public class Worker(
    IServiceScopeFactory scopeFactory)
    : BackgroundService
{
}
```

```csharp
using var scope = scopeFactory.CreateScope();
```

Clear and shows that you only need to create scopes.

---

### Option 2

```csharp
public class Worker(
    IServiceProvider serviceProvider)
    : BackgroundService
{
}
```

```csharp
using var scope = serviceProvider.CreateScope();
```

Also correct.

Useful when you need to resolve different services.

---

# Which is Better?

For a `BackgroundService` that only needs to create a scope,

```csharp
IServiceScopeFactory
```

is slightly clearer because its purpose is only to create scopes.

If you also need to resolve many different services, using

```csharp
IServiceProvider
```

is also a common and valid approach.

---

# Summary

- `BackgroundService` = **Singleton**
- `DbContext` = **Scoped**
- Singleton **cannot directly use** Scoped services.
- Create a new scope before using `DbContext`.
- `IServiceScopeFactory` is used to create scopes.
- `IServiceProvider` is the DI container and can also create scopes.
- Both approaches are correct and widely used.