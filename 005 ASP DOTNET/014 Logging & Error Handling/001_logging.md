# Logging in ASP.NET Core

---

# What is Logging?

Logging means recording application information.

Used to store:
- Errors
- Warnings
- Requests
- Debug information
- Application events

---

# Why Logging Important?

Used for:
- Debugging
- Monitoring
- Tracking errors
- Production support
- Performance analysis

---

# Example Logs

```text
Application Started

User Logged In

Database Error

API Request Received
```

---

# Logging Flow

```text
Application Event
        ↓
Logger Captures Information
        ↓
Logs Stored
        ↓
Developer Reads Logs
```

---

# Types of Logging

- ILogger
- Console Logging
- Debug Logging
- Serilog
- NLog

---

# 1. ILogger

---

# What is ILogger?

`ILogger` is built-in logging interface in ASP.NET Core.

Used to write logs.

---

# Namespace

```cs
using Microsoft.Extensions.Logging;
```

---

# Using ILogger in Controller

```cs
using Microsoft.AspNetCore.Mvc;

public class EmployeeController : Controller
{
    private readonly ILogger<EmployeeController> _logger;

    public EmployeeController(ILogger<EmployeeController> logger)
    {
        _logger = logger;
    }

    public IActionResult Index()
    {
        _logger.LogInformation("Employee Page Loaded");

        return View();
    }
}
```

---

# Explanation

---

# ILogger<EmployeeController>

```cs
ILogger<EmployeeController>
```

- ASP.NET Core injects logger automatically.

---

# _logger.LogInformation()

```cs
_logger.LogInformation("Employee Page Loaded");
```

- Writes information log.

---

# Output Example

```text
info:
EmployeeController[0]
Employee Page Loaded
```

---

# Log Levels

| Log Level | Purpose |
|---|---|
| Trace | Detailed tracking |
| Debug | Debugging |
| Information | General information |
| Warning | Warning message |
| Error | Errors |
| Critical | Serious failure |

---

# Example

## Information

```cs
_logger.LogInformation("Data Loaded");
```

---

## Warning

```cs
_logger.LogWarning("Low Memory");
```

---

## Error

```cs
_logger.LogError("Database Failed");
```

---

## Critical

```cs
_logger.LogCritical("Server Crashed");
```

---

# Logging Exception

```cs
try
{
    int x = 0;
}
catch(Exception ex)
{
    _logger.LogError(ex, "Exception Occurred");
}
```

---

# Output

```text
Exception Occurred
Stack Trace...
```

---

# ILogger Flow

```text
Application Event
        ↓
     ILogger
        ↓
Logging Provider
        ↓
Console/File/Database
```

---

# 2. Console Logging


# What is Console Logging?

- Writes logs into terminal/console.


# Program.cs Setup

```cs
builder.Logging.AddConsole();
```

---

# Complete Example

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Logging.AddConsole();

var app = builder.Build();

app.Run();
```

---

# Output

```text
info: Application Started
```

---

# Purpose

Used for:
- Development
- Debugging
- Local testing

---

# Console Logging Flow

```text
Application Event
        ↓
     ILogger
        ↓
Console Provider
        ↓
Terminal Output
```

---

# 3. Debug Logging

---

# What is Debug Logging?

Writes logs into:
- Visual Studio Debug Window

---

# Program.cs Setup

```cs
builder.Logging.AddDebug();
```

---

# Example

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Logging.AddDebug();

var app = builder.Build();

app.Run();
```

---

# Output Location

```text
Visual Studio
    ↓
Output Window
    ↓
Debug
```

---

# Purpose

Used during:
- Development
- Debugging

---

# Difference

| Console Logging | Debug Logging |
|---|---|
| Terminal Output | Visual Studio Output |

---

# 4. Serilog

---

# What is Serilog?

Serilog is advanced third-party logging framework.

---

# Features

- File logging
- Database logging
- Structured logging
- JSON logging
- Better production logging

---

# Install Packages

```bash
dotnet add package Serilog.AspNetCore

dotnet add package Serilog.Sinks.Console

dotnet add package Serilog.Sinks.File
```

---

# Program.cs Setup

```cs
using Serilog;

var builder =
    WebApplication.CreateBuilder(args);

Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("Logs/log.txt")
    .CreateLogger();

builder.Host.UseSerilog();

var app = builder.Build();

app.Run();
```

---

# Explanation

---

# WriteTo.Console()

```cs
.WriteTo.Console()
```

Writes logs to terminal.

---

# WriteTo.File()

```cs
.WriteTo.File("Logs/log.txt")
```

Writes logs into file.

---

# Log File Structure

```text
Project
│
├── Logs/
│      └── log.txt
```

---

# Using ILogger with Serilog

```cs
_logger.LogInformation("Data Loaded");
```

Still works.

But Serilog stores logs.

---

# Example Log File

```text
2026-01-01
Information
Employee Loaded
```

---

# Serilog Advantages

- Production ready
- File logs
- JSON logs
- Better monitoring

---

# Structured Logging

```cs
_logger.LogInformation(
    "User {UserId} logged in", 5);
```

---

# Output

```text
User 5 logged in
```

---

# Serilog Flow

```text
Application Event
        ↓
ILogger
        ↓
Serilog
        ↓
Console/File/Database
```

---

# 5. NLog

---

# What is NLog?

NLog is another advanced logging framework.

---

# Features

- File logging
- Database logging
- Email logging
- Production logging

---

# Install Packages

```bash
dotnet add package NLog.Web.AspNetCore
```

---

# Program.cs Setup

```cs
using NLog.Web;

var builder = WebApplication.CreateBuilder(args);

builder.Logging.ClearProviders();
builder.Host.UseNLog();

var app = builder.Build();

app.Run();
```

---

# NLog Configuration File

```text
nlog.config
```

---

# Example nlog.config

```xml
<nlog>
  <targets>
    <target name="logfile"
            xsi:type="File"
            fileName="logs/log.txt" />
  </targets>

  <rules>
    <logger name="*" 
            minlevel="Info"
            writeTo="logfile" />
  </rules>
</nlog>
```

---

# Log File Output

```text
Info: User Logged In
Error: Database Failed
```

---

# NLog Advantages

- Fast logging
- File support
- Database support
- Enterprise logging

---

# Serilog vs NLog

| Serilog | NLog |
|---|---|
| Structured logging | Traditional logging |
| JSON support | XML config |
| Modern | Mature |

---

# Logging Providers

| Provider | Output |
|---|---|
| Console | Terminal |
| Debug | Visual Studio |
| Serilog | File/DB/Console |
| NLog | File/DB/Email |

---

# Complete Logging Example

```cs
using Serilog;

var builder = WebApplication.CreateBuilder(args);

builder.Logging.AddConsole();

builder.Logging.AddDebug();

Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("Logs/log.txt")
    .CreateLogger();

builder.Host.UseSerilog();

builder.Services.AddControllers();

var app = builder.Build();

app.MapControllers();

app.Run();
```

---

# Logging in Middleware

```cs
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    private readonly ILogger<LoggingMiddleware>
        _logger;

    public LoggingMiddleware(
        RequestDelegate next,
        ILogger<LoggingMiddleware> logger)
    {
        _next = next;

        _logger = logger;
    }

    public async Task Invoke(HttpContext context)
    {
        _logger.LogInformation(
            $"Request: {context.Request.Path}");

        await _next(context);

        _logger.LogInformation(
            $"Response: {context.Response.StatusCode}");
    }
}
```

---

# Logging Flow in Middleware

```text
Request Comes
      ↓
Log Request
      ↓
Controller Executes
      ↓
Log Response
```

---

# Logging Best Practices

- Use Error logs for exceptions
- Use Warning logs carefully
- Avoid sensitive data in logs
- Use structured logging

---

# Common Production Logs

- API Requests
- Database Errors
- Login Attempts
- Unauthorized Access
- Server Failures

---

# Complete Logging Flow

```text
Application Event
        ↓
ILogger
        ↓
Logging Provider
        ↓
Console/File/Database
        ↓
Developer Reads Logs
```

---

# Real-Life Analogy

| Logging Part | Real Life |
|---|---|
| ILogger | CCTV Camera |
| Console Logging | Live Monitor |
| Debug Logging | Developer Screen |
| Serilog | Advanced Security System |
| NLog | Enterprise Monitoring System |
| Log File | Security Recording |




--------------
extra need to fix: later I do it:

# Additional Topics to Cover

---

# 1. ILoggerFactory

## What is ILoggerFactory?

`ILoggerFactory` creates `ILogger` instances.

Example

```csharp
public class EmployeeService
{
    private readonly ILogger _logger;

    public EmployeeService(ILoggerFactory loggerFactory)
    {
        _logger = loggerFactory.CreateLogger<EmployeeService>();
    }
}
```

Used when you need to create loggers dynamically.

---

# 2. ILoggerProvider

## What is ILoggerProvider?

A logging provider determines where logs are written.

Examples

- Console
- Debug
- EventLog
- EventSource
- Serilog
- NLog

Flow

```
ILogger

↓

ILoggerProvider

↓

Console / File / Database
```

---

# 3. Default Logging Providers

`WebApplication.CreateBuilder()` automatically adds:

- Console
- Debug
- EventSource
- EventLog (Windows)

You don't always need:

```csharp
builder.Logging.AddConsole();
```

unless you removed providers.

---

# 4. ClearProviders()

```csharp
builder.Logging.ClearProviders();
```

Removes all default providers.

Example

Before

```
Console

Debug

EventSource
```

After

```
None
```

---

# 5. AddConsole()

```csharp
builder.Logging.AddConsole();
```

Adds Console provider again.

---

# 6. SetMinimumLevel()

```csharp
builder.Logging.SetMinimumLevel(
    LogLevel.Warning);
```

Only logs

```
Warning

Error

Critical
```

---

# 7. AddFilter()

```csharp
builder.Logging.AddFilter(
    "Microsoft",
    LogLevel.Warning);
```

Filters logs from specific categories.

---

# 8. appsettings.json Logging

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting": "Information"
    }
  }
}
```

Controls logging without changing code.

---

# 9. EventId

```csharp
logger.LogInformation(
    new EventId(1001, "Login"),
    "User Logged In");
```

Useful for log filtering.

---

# 10. Structured Logging

Good

```csharp
logger.LogInformation(
    "Employee {Id} Created",
    id);
```

Bad

```csharp
logger.LogInformation(
    "Employee " + id + " Created");
```

Benefits

- Searchable
- Structured
- JSON friendly

---

# 11. BeginScope()

```csharp
using(logger.BeginScope(
    "RequestId:{Id}", requestId))
{
    logger.LogInformation("Started");
}
```

Groups related logs.

---

# 12. Category Logging

```csharp
ILogger<EmployeeService>
```

Category becomes

```
EmployeeService
```

Useful for filtering logs.

---

# 13. Exception Logging

```csharp
try
{

}
catch(Exception ex)
{
    logger.LogError(
        ex,
        "Database Error");
}
```

Always pass the exception object.

---

# 14. Serilog Minimum Level

```csharp
.MinimumLevel.Information()

.MinimumLevel.Warning()

.MinimumLevel.Error()

.MinimumLevel.Fatal()
```

---

# 15. Serilog Rolling Files

```csharp
.WriteTo.File(
    "Logs/log-.txt",
    rollingInterval:
    RollingInterval.Day)
```

Creates

```
log-20260721.txt

log-20260722.txt
```

Automatically.

---

# 16. Serilog Enrichers

Adds extra information.

```csharp
.Enrich.WithMachineName()

.Enrich.WithThreadId()

.Enrich.WithProcessId()
```

---

# 17. Serilog Sinks

Common sinks

- Console
- File
- Seq
- SQL Server
- PostgreSQL
- MySQL
- MongoDB
- Elasticsearch
- Azure
- Email

---

# 18. NLog Targets

Targets

- File
- Console
- Database
- Mail
- Network

---

# 19. log4net

Another logging library.

Supports

- File
- Rolling File
- Console
- Database
- SMTP

---

# 20. Built-in Provider Comparison

| Provider | File | Purpose |
|----------|------|----------|
| Console | ❌ | Terminal |
| Debug | ❌ | Visual Studio |
| EventLog | ❌ | Windows Event Viewer |
| EventSource | ❌ | Diagnostics |

---

# 21. Third-party Comparison

| Library | File | JSON | Structured |
|----------|------|------|-------------|
| Serilog | ✅ | ✅ | ✅ |
| NLog | ✅ | Limited | Partial |
| log4net | ✅ | ❌ | ❌ |

---

# 22. Logging in Services

```csharp
public class EmployeeService
{
    private readonly ILogger<EmployeeService> logger;

    public EmployeeService(
        ILogger<EmployeeService> logger)
    {
        this.logger = logger;
    }
}
```

---

# 23. Logging in BackgroundService

```csharp
public class Worker(
    ILogger<Worker> logger)
    : BackgroundService
{
}
```

---

# 24. Production Best Practices

- Use `ILogger<T>`
- Use structured logging
- Log exceptions
- Avoid sensitive information
- Use rolling files
- Keep log levels appropriate
- Archive old logs

---

# 25. Common Interview Questions

- What is ILogger?
- What is ILoggerFactory?
- What is ILoggerProvider?
- What is a logging provider?
- Explain all log levels.
- What is structured logging?
- Difference between Console and Debug logging?
- Why use Serilog?
- Why use NLog?
- What is rolling file logging?
- What is EventId?
- What is BeginScope()?
- What is appsettings.json logging?
- Difference between Error and Critical?
- What does ClearProviders() do?