# Hosted Services in .NET

### Types of Hosted Services

There are two ways to create a Hosted Service.

**1. IHostedService:**
- Interface
- Manual lifecycle implementation.

**2. BackgroundService:**
- Abstract class
- Recommended approach.
- Automatically implements IHostedService.


[IHostedService](#ihostedservice) | [BackgroundService](#backgroundservice-1) (Use this strictly) |

-------

# IHostedService
- A class implementing this interface becomes a Hosted Service.
```cs
public interface IHostedService
{
    Task StartAsync(CancellationToken cancellationToken);

    Task StopAsync(CancellationToken cancellationToken);
}
```

**Responsibilities:**
You implement:
- Startup
- Shutdown
Everything is manual.


### StartAsync()
- Called exactly once.

**Example:**
```csharp
public Task StartAsync(CancellationToken token)
{
    Console.WriteLine("Started");

    return Task.CompletedTask;
}
```

### StopAsync()
- Called once before shutdown.

**Example:**

```csharp
public Task StopAsync(CancellationToken token)
{
    Console.WriteLine("Stopped");

    return Task.CompletedTask;
}
```


**Lifecycle:**

```
Application Starts
        │
StartAsync()
        │
Service Running
        │
Application Stops
        │
StopAsync()
        │
Dispose()
```


**Complete Example:**

```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

public class MyHostedService : IHostedService
{
    private readonly ILogger<MyHostedService> _logger;

    public MyHostedService(ILogger<MyHostedService> logger)
    {
        _logger = logger;
    }

    public Task StartAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("MyHostedService started at: {Time}", DateTimeOffset.Now);

        return Task.CompletedTask;
    }

    public Task StopAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("MyHostedService stopped at: {Time}", DateTimeOffset.Now);

        return Task.CompletedTask;
    }
}
```

**Registration:** `Program.cs`
```csharp
builder.Services.AddHostedService<MyHostedService>();
```

**Suitable for:**
- SFTP Connection
- Usually no infinite loop exists.

---


# BackgroundService

- BackgroundService is an abstract class.
- It already implements:
    - IHostedService
- You only override:
    - `ExecuteAsync()`

**Function Override:**
---|-------------
Method | Override?
---|-----------
Constructor | Yes
ExecuteAsync(CancellationToken) | Required
StartAsync(CancellationToken) | Optional
StartAsync(cancellationToken) | Optional
StopAsync(CancellationToken) | Optional
Dispose() | Optional


## ExecuteAsync()

```csharp
protected override Task ExecuteAsync(CancellationToken stoppingToken)
```
- This method runs continuously.


**Example:**
```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;

    public Worker(ILogger<Worker> logger)
    {
        _logger = logger;
    }

    public override async Task StartAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("StartAsync");

        await base.StartAsync(cancellationToken);
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogInformation("ExecuteAsync Started");

        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogInformation("Working...");

            await Task.Delay(1000, stoppingToken);
        }

        _logger.LogInformation("ExecuteAsync Ended");
    }

    public override async Task StopAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("StopAsync");

        await base.StopAsync(cancellationToken);
    }

    public override void Dispose()
    {
        _logger.LogInformation("Dispose");

        base.Dispose();
    }
}
```


### Worker Service Project Structure

```
WorkerServiceApp/
│
├── Program.cs
├── Worker.cs
├── appsettings.json
├── appsettings.Development.json
└── Properties
```


### Program.cs

```csharp
using WorkerServiceApp;

var builder = Host.CreateApplicationBuilder(args);

builder.Services.AddHostedService<Worker>();

var host = builder.Build();

host.Run();
```


### Worker.cs

```csharp
public class Worker : BackgroundService
{
    protected override async Task ExecuteAsync(
        CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            Console.WriteLine(DateTime.Now);

            await Task.Delay(1000, stoppingToken);
        }
    }
}
```


# Dependency Injection

Hosted Services fully support DI.

Example

```csharp
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;

    public Worker(ILogger<Worker> logger)
    {
        _logger = logger;
    }

    protected override async Task ExecuteAsync(CancellationToken token)
    {
        while (!token.IsCancellationRequested)
        {
            _logger.LogInformation("Running");

            await Task.Delay(1000, token);
        }
    }
}
```

---

# Injecting Multiple Services

```csharp
public Worker(
    ILogger<Worker> logger,
    IConfiguration configuration,
    IServiceProvider provider)
{
}
```

---

# CancellationToken

Purpose

Gracefully stop background work.

```cs
while(!token.IsCancellationRequested)
{
}
```

Without checking it,

the service cannot stop correctly.

---

# Why use CancellationToken?

Without cancellation,

```
while(true)
{
}
```

Application cannot exit safely.

Correct

```csharp
while (!token.IsCancellationRequested)
{
}
```

---

# Scoped Services

Hosted Services are Singleton.

Scoped services cannot be injected directly.

Wrong

```csharp
public Worker(AppDbContext db)
{

}
```

**Correct**
```csharp
public Worker(IServiceScopeFactory scopeFactory)
{

}
```

---

Create Scope

```csharp
using var scope = scopeFactory.CreateScope();

var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();
```

---

# Timers

Instead of while loop,

you can use Timer.

Example

```csharp
private Timer? timer;

public Task StartAsync(CancellationToken token)
{
    timer = new Timer(
        DoWork,
        null,
        TimeSpan.Zero,
        TimeSpan.FromSeconds(5));

    return Task.CompletedTask;
}
```

---

# PeriodicTimer (.NET 6+)

Better alternative.

```csharp
var timer =
new PeriodicTimer(TimeSpan.FromSeconds(5));

while(await timer.WaitForNextTickAsync(token))
{
    Console.WriteLine("Tick");
}
```

Advantages

- Async
- No overlap
- Cleaner
- Cancellation support

---

# Logging

Use ILogger.

```csharp
_logger.LogInformation("Worker Started");
```

Levels

- Trace
- Debug
- Information
- Warning
- Error
- Critical

---

# Reading Configuration

appsettings.json

```json
{
  "Interval": 5
}
```

Inject IConfiguration.

```csharp
var seconds =
_configuration.GetValue<int>("Interval");
```

---

# Exception Handling

Always protect background loops.

```csharp
try
{
}
catch(Exception ex)
{
    _logger.LogError(ex.Message);
}
```

---

# Graceful Shutdown

When application exits,

Host sends cancellation.

```
CancellationToken

↓

Loop exits

↓

StopAsync()

↓

Dispose()
```

Never call

```
Environment.Exit()
```

inside Worker.

---

# Multiple Hosted Services

Register multiple workers.

```csharp
builder.Services.AddHostedService<EmailWorker>();

builder.Services.AddHostedService<QueueWorker>();

builder.Services.AddHostedService<CacheWorker>();
```

Execution

```
Application

↓

EmailWorker

↓

QueueWorker

↓

CacheWorker
```

All run independently.

---

# Common Use Cases

- Email Sender
- Notification Service
- Kafka Consumer
- RabbitMQ Consumer
- Azure Service Bus
- Redis Subscriber
- File Monitor
- Cache Refresh
- Database Cleanup
- Report Generator
- Cron-like Scheduler
- Health Checker
- Metrics Collector
- IoT Device Listener
- Background Image Processing

---

# IHostedService vs BackgroundService

| Feature | IHostedService | BackgroundService |
|----------|---------------|-------------------|
| Type | Interface | Abstract Class |
| StartAsync | Must implement | Already implemented |
| StopAsync | Must implement | Already implemented |
| ExecuteAsync | Not available | Override |
| Infinite Loop | Manual | Built-in |
| Code | More | Less |
| Lifecycle | Manual | Automatic |
| Recommended | Rarely | Yes |
| Best Use | Startup/Shutdown tasks | Long-running work |

---

# Advantages of BackgroundService

- Simple API
- Automatic lifecycle
- Built-in cancellation
- Supports async programming
- Integrates with Dependency Injection
- Supports logging
- Easy configuration access
- Ideal for long-running services
- Reduces boilerplate code
- Recommended by Microsoft

---

# Best Practices

- Prefer `BackgroundService` for long-running tasks.
- Always observe the `CancellationToken`.
- Avoid `Thread.Sleep`; use `Task.Delay`.
- Catch and log exceptions inside the execution loop.
- Use `PeriodicTimer` for recurring work when appropriate.
- Create a service scope before resolving scoped services.
- Keep each hosted service focused on a single responsibility.
- Use `ILogger<T>` instead of `Console.WriteLine` in production.
- Read settings from configuration rather than hard-coding values.
- Dispose unmanaged resources properly.

---