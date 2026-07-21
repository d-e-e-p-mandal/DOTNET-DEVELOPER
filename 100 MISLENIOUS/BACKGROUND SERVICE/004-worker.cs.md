
[New](#worker) | [Old]

# Worker.cs (Complete Background Service - .NET 6/7/8/9)

```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

namespace EmployeeWorkerService;

public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;

    public Worker(ILogger<Worker> logger)
    {
        _logger = logger;
    }

    // Called when the service starts
    public override async Task StartAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("Worker Service is starting at: {time}", DateTimeOffset.Now);

        await base.StartAsync(cancellationToken);
    }

    // Main background task
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogInformation("Background task started.");

        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);

            // Your background work goes here
            // Example:
            // await SendEmails();
            // await SyncDatabase();
            // await CallExternalApi();

            await Task.Delay(TimeSpan.FromSeconds(5), stoppingToken);
        }

        _logger.LogInformation("Background task is stopping.");
    }

    // Called when the service is stopping
    public override async Task StopAsync(CancellationToken cancellationToken)
    {
        _logger.LogInformation("Worker Service is stopping at: {time}", DateTimeOffset.Now);

        await base.StopAsync(cancellationToken);
    }

    // Called before the service is disposed
    public override void Dispose()
    {
        _logger.LogInformation("Worker Service disposed.");

        base.Dispose();
    }
}
```

---

# Explanation

## `using Microsoft.Extensions.Hosting;`

Provides:

- `BackgroundService`
- `IHostedService`

---

## `using Microsoft.Extensions.Logging;`

Provides logging support.

Example:

```csharp
_logger.LogInformation("Worker started.");
```

---

## `public class Worker : BackgroundService`

Creates a background service.

`BackgroundService` already implements `IHostedService`.

You only need to override the methods you want.

---

## `ILogger<Worker>`

```csharp
private readonly ILogger<Worker> _logger;
```

Creates a logger for this class.

Used to write logs.

---

## Constructor

```csharp
public Worker(ILogger<Worker> logger)
{
    _logger = logger;
}
```

Dependency Injection automatically provides the logger.

---

## `StartAsync()`

```csharp
public override async Task StartAsync(CancellationToken cancellationToken)
```

Called **once** when the application starts.

Typical use cases:

- Initialize resources
- Open connections
- Log startup
- Validate configuration

Always call:

```csharp
await base.StartAsync(cancellationToken);
```

because it starts the background execution (`ExecuteAsync`).

---

## `ExecuteAsync()`

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
```

The main background task.

Runs automatically after `StartAsync()`.

Normally contains:

```csharp
while (!stoppingToken.IsCancellationRequested)
{
    // Background work
}
```

Examples:

- Send emails
- Read messages from a queue
- Poll an API
- Process files
- Clean old data
- Generate reports

---

## `CancellationToken`

```csharp
stoppingToken
```

Signals that the application is shutting down.

When cancellation is requested:

```csharp
stoppingToken.IsCancellationRequested
```

becomes `true`, allowing the loop to exit gracefully.

---

## `Task.Delay()`

```csharp
await Task.Delay(TimeSpan.FromSeconds(5), stoppingToken);
```

Waits for 5 seconds before the next iteration.

Passing `stoppingToken` allows the delay to end immediately if the application is stopping.

---

## `StopAsync()`

```csharp
public override async Task StopAsync(CancellationToken cancellationToken)
```

Called once when the application is shutting down.

Typical use cases:

- Flush logs
- Save state
- Close database connections
- Stop timers
- Release resources

Always call:

```csharp
await base.StopAsync(cancellationToken);
```

to allow the base class to complete shutdown.

---

## `Dispose()`

```csharp
public override void Dispose()
```

Called when the `Worker` object is being disposed.

Use it to release unmanaged resources if needed.

Always call:

```csharp
base.Dispose();
```

---

# Complete Lifecycle

```text
Application Starts
        │
        ▼
Program.cs
        │
        ▼
AddHostedService<Worker>()
        │
        ▼
Worker Constructor
        │
        ▼
StartAsync()
        │
        ▼
base.StartAsync()
        │
        ▼
ExecuteAsync()
        │
        ▼
while (!stoppingToken.IsCancellationRequested)
        │
        ▼
Background Work
        │
        ▼
Task.Delay()
        │
        ▼
(repeats until shutdown)
        │
        ▼
Application Stops
        │
        ▼
StopAsync()
        │
        ▼
Dispose()
        │
        ▼
Worker Destroyed
```

# Notes

- `ExecuteAsync()` is the **only required method** to override.
- `StartAsync()`, `StopAsync()`, and `Dispose()` are **optional** and are overridden only when you need custom startup, shutdown, or cleanup logic.
- `BackgroundService` already implements `IHostedService`, so you usually inherit from `BackgroundService` instead of implementing `IHostedService` directly.


# Worker.cs Using Primary Constructor (.NET 8 / C# 12)

```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

namespace EmployeeWorkerService;

public class Worker(ILogger<Worker> logger) : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);

            await Task.Delay(5000, stoppingToken);
        }
    }
}
```

---

# Explanation

## Class Declaration

```csharp
public class Worker(ILogger<Worker> logger) : BackgroundService
```

This is called a **Primary Constructor**.

Introduced in **C# 12 (.NET 8)**.

Instead of writing a constructor separately, the constructor parameter is declared directly after the class name.

---

## `Worker(...)`

```csharp
Worker(ILogger<Worker> logger)
```

Defines the constructor.

Equivalent to:

```csharp
public Worker(ILogger<Worker> logger)
{
    ...
}
```

---

## `ILogger<Worker> logger`

```csharp
ILogger<Worker> logger
```

Dependency Injection automatically provides the logger.

You can use `logger` anywhere inside the class.

Example:

```csharp
logger.LogInformation("Application Started");
```

No private field is required unless you want one.

---

## `: BackgroundService`

```csharp
: BackgroundService
```

Inherits from `BackgroundService`.

`BackgroundService` already implements `IHostedService`.

---

## `ExecuteAsync()`

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
```

The main background method.

Starts automatically when the application starts.

---

## `CancellationToken`

```csharp
stoppingToken
```

Indicates whether the application is shutting down.

---

## `while`

```csharp
while (!stoppingToken.IsCancellationRequested)
```

Runs continuously until the application stops.

---

## Logging

```csharp
logger.LogInformation("Worker running...");
```

Writes a log message.

---

## Delay

```csharp
await Task.Delay(5000, stoppingToken);
```

Waits for 5 seconds before running again.

---

# Traditional Constructor vs Primary Constructor

## Traditional Constructor (Before C# 12)

```csharp
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;

    public Worker(ILogger<Worker> logger)
    {
        _logger = logger;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogInformation("Running...");
    }
}
```

---

## Primary Constructor (C# 12)

```csharp
public class Worker(ILogger<Worker> logger) : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        logger.LogInformation("Running...");
    }
}
```

---

# Difference

| Traditional Constructor | Primary Constructor |
|-------------------------|---------------------|
| Separate constructor required | Constructor written in class declaration |
| Usually needs a private field (`_logger`) | Parameter is available directly in the class |
| More code | Less code |
| Works in older C# versions | Requires C# 12 (.NET 8 or later) |
| Most existing projects use this style | Common in new .NET 8+ templates |

---

# Execution Flow

```text
Program.cs
        │
        ▼
AddHostedService<Worker>()
        │
        ▼
Dependency Injection creates Worker
        │
        ▼
ILogger<Worker> injected into primary constructor
        │
        ▼
ExecuteAsync()
        │
        ▼
while loop starts
        │
        ▼
logger.LogInformation(...)
        │
        ▼
Task.Delay()
        │
        ▼
Repeat until application stops
```

# Notes

- `public class Worker(ILogger<Worker> logger) : BackgroundService` is simply a shorter way of writing a constructor.
- It is a **C# 12 language feature** called a **primary constructor**.
- Functionally, it behaves the same as the traditional constructor; it just reduces boilerplate code.




------
------

## Old Structure:

# `using` Statements in `Worker.cs`

```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;
```

These are the only namespaces required for a basic `Worker.cs`.

---

# 1. `using Microsoft.Extensions.Hosting;`

Provides hosting classes for background services.

Main types:

- `BackgroundService`
- `IHostedService`
- `IHost`
- `IHostApplicationLifetime`

Example:

```csharp
public class Worker : BackgroundService
{
}
```

Without this namespace:

```csharp
BackgroundService
```

will not be recognized.

---

# 2. `using Microsoft.Extensions.Logging;`

Provides logging functionality.

Main types:

- `ILogger`
- `ILogger<T>`
- `LoggerFactory`

Example:

```csharp
logger.LogInformation("Worker Started");
```

Without this namespace:

```csharp
ILogger<Worker>
```

and

```csharp
LogInformation()
```

will not be recognized.

---

# Other Common `using` Statements (Optional)

## Tasks

```csharp
using System.Threading.Tasks;
```

Provides:

- `Task`
- `Task<T>`

Usually included automatically by **Implicit Usings** in modern .NET projects.

---

## Cancellation

```csharp
using System.Threading;
```

Provides:

- `CancellationToken`

Usually included automatically.

---

## Date & Time

```csharp
using System;
```

Provides:

- `DateTime`
- `DateTimeOffset`
- `TimeSpan`

Usually included automatically.

---

# Typical Worker.cs

```csharp
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

namespace EmployeeWorkerService;

public class Worker(ILogger<Worker> logger) : BackgroundService
{
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);

            await Task.Delay(TimeSpan.FromSeconds(5), stoppingToken);
        }
    }
}
```

---

# Where do `Task`, `CancellationToken`, and `DateTimeOffset` come from?

You may notice there are no `using` statements for these types. In modern .NET (6+), the project template enables **Implicit Usings** by default in the `.csproj` file:

```xml
<ImplicitUsings>enable</ImplicitUsings>
```

This automatically imports common namespaces such as:

- `System`
- `System.Threading`
- `System.Threading.Tasks`

So you can use:

```csharp
Task
CancellationToken
DateTimeOffset
TimeSpan
```

without writing their `using` statements manually.

If **Implicit Usings** are disabled, you would need:

```csharp
using System;
using System.Threading;
using System.Threading.Tasks;
```