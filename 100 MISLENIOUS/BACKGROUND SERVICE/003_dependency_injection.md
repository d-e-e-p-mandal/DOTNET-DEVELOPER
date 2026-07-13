# Dependency Injection in Background Services:

```csharp
builder.Services.AddHostedService<Worker>();
```


## Constructor Injection:

```csharp
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;
    private readonly IConfiguration _configuration;

    public Worker(ILogger<Worker> logger, IConfiguration configuration)
    {
        _logger = logger;
        _configuration = configuration;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogInformation("Running");

            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

---

## Using IServiceScopeFactory (Recommended for Scoped Services)

```csharp
public class Worker : BackgroundService
{
    private readonly IServiceScopeFactory _scopeFactory;

    public Worker(IServiceScopeFactory scopeFactory)
    {
        _scopeFactory = scopeFactory;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            using IServiceScope scope = _scopeFactory.CreateScope();

            var service = scope.ServiceProvider.GetRequiredService<IMyScopedService>();

            await service.DoWorkAsync();

            await Task.Delay(5000, stoppingToken);
        }
    }
}
```


## Using DbContext (Correct)

```csharp
public class Worker : BackgroundService
{
    private readonly IServiceScopeFactory _scopeFactory;

    public Worker(IServiceScopeFactory scopeFactory)
    {
        _scopeFactory = scopeFactory;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            using IServiceScope scope = _scopeFactory.CreateScope();

            var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();

            var employees = await db.Employees.ToListAsync();

            await Task.Delay(5000, stoppingToken);
        }
    }
}
```


## GetRequiredService()
```csharp
var service = scope.ServiceProvider.GetRequiredService<IMyService>();
```

## GetService()
```csharp
var service = scope.ServiceProvider.GetService<IMyService>();
```

-----
==========


## Common Constructor Injections

```csharp
public Worker(
    ILogger<Worker> logger,
    IConfiguration configuration,
    IServiceScopeFactory scopeFactory)
{
}
```

----------
=============


## Mistake:

## Wrong (Don't Inject Scoped Service Directly)

```csharp
public class Worker : BackgroundService
{
    private readonly AppDbContext _db;

    public Worker(AppDbContext db)
    {
        _db = db;
    }

    protected override async Task ExecuteAsync(
        CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            var employees = await _db.Employees.ToListAsync();

            await Task.Delay(5000, stoppingToken);
        }
    }
}
```