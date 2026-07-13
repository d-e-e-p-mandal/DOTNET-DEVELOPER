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