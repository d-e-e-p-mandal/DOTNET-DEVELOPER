# .NET Logging Cheat Sheet (Background Service / Web API)

## What is Logging?

Logging is the process of recording application events.

Uses:

- Debugging
- Error Tracking
- Monitoring
- Performance Analysis
- Auditing
- Troubleshooting
- Production Monitoring

---

# Logging Flow

```
Application

      │

      ▼

ILogger<T>

      │

      ▼

Logging Provider

      │

      ├── Console
      ├── Debug
      ├── EventLog
      ├── EventSource
      ├── Serilog
      ├── NLog
      ├── log4net
      ├── SQL Server
      ├── Seq
      ├── Elasticsearch
      └── Cloud
```

---

# ILogger

Main logging interface.

```csharp
public class Worker(ILogger<Worker> logger)
    : BackgroundService
{
}
```

Dependency Injection automatically injects the logger.

---

# Log Methods

```csharp
logger.LogTrace("");

logger.LogDebug("");

logger.LogInformation("");

logger.LogWarning("");

logger.LogError("");

logger.LogCritical("");
```

---

# Log Levels

| Level | Value | Purpose |
|---------|------|----------|
| Trace | 0 | Most detailed |
| Debug | 1 | Development |
| Information | 2 | Normal logs |
| Warning | 3 | Unexpected but recoverable |
| Error | 4 | Operation failed |
| Critical | 5 | Application failure |
| None | 6 | Disable logging |

---

# Structured Logging

Bad

```csharp
logger.LogInformation("User " + id + " Logged In");
```

Good

```csharp
logger.LogInformation(
    "User {UserId} Logged In",
    id);
```

Benefits

- Searchable
- JSON Friendly
- Structured Data

---

# Event Id

```csharp
logger.LogInformation(
    new EventId(1001, "Login"),
    "User Logged In");
```

Useful for filtering logs.

---

# Exception Logging

```csharp
try
{

}
catch(Exception ex)
{
    logger.LogError(ex,
        "Database Error");
}
```

---

# Logging Providers

A provider decides where logs are written.

---

# Built-in Providers

## Console

```csharp
builder.Logging.AddConsole();
```

Output

```
Terminal

PowerShell

Docker Logs
```

File?

❌

---

## Debug

```csharp
builder.Logging.AddDebug();
```

Output

```
Visual Studio

Output Window
```

File?

❌

---

## Event Log

```csharp
builder.Logging.AddEventLog();
```

Output

```
Windows Event Viewer
```

Windows Only

---

## EventSource

```csharp
builder.Logging.AddEventSourceLogger();
```

Output

```
ETW

Diagnostic Tools
```

---

# Clear Providers

```csharp
builder.Logging.ClearProviders();
```

Removes all providers.

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

# Add Providers

```csharp
builder.Logging.AddConsole();

builder.Logging.AddDebug();
```

Now logs go to

- Console
- Debug Window

---

# appsettings.json Logging

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "System": "Warning"
    }
  }
}
```

---

# Minimum Log Level

Program.cs

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

# Category Filtering

```csharp
builder.Logging.AddFilter(
    "Microsoft",
    LogLevel.Warning);
```

---

# Begin Scope

```csharp
using(logger.BeginScope(
    "RequestId:{Id}",1))
{
    logger.LogInformation("Started");
}
```

Groups related logs.

---

# Common Message Template

```csharp
logger.LogInformation(
    "Employee {Id} Created",
    employeeId);
```

---

# Built-in Logging Limitations

Cannot

- Create log.txt
- Daily Log Files
- JSON Files
- SQL Logging
- Elasticsearch
- Seq
- Cloud Sinks

Need third-party libraries.

---

# Third Party Libraries

- Serilog
- NLog
- log4net

---

# Serilog

Most popular modern logging library.

Packages

```bash
dotnet add package Serilog.AspNetCore

dotnet add package Serilog.Sinks.File
```

---

## Configuration

```csharp
using Serilog;

Log.Logger =
    new LoggerConfiguration()

    .MinimumLevel.Information()

    .WriteTo.Console()

    .WriteTo.File(
        "Logs/log-.txt",
        rollingInterval:
        RollingInterval.Day)

    .CreateLogger();
```

---

## Connect to .NET

```csharp
builder.Services.AddSerilog();
```

---

## Output

```
Logs

    log-20260721.txt

    log-20260722.txt
```

---

## Serilog Minimum Level

```csharp
.MinimumLevel.Debug()

.MinimumLevel.Information()

.MinimumLevel.Warning()

.MinimumLevel.Error()

.MinimumLevel.Fatal()
```

---

## Override

```csharp
.MinimumLevel.Override(
    "Microsoft",
    LogEventLevel.Warning)
```

---

## Enrichers

Adds extra information.

```csharp
.Enrich.FromLogContext()

.Enrich.WithMachineName()

.Enrich.WithThreadId()

.Enrich.WithProcessId()
```

Output

```
MachineName

ThreadId

ProcessId
```

---

## Common Sinks

```
Console

File

Seq

SQL Server

MySQL

PostgreSQL

MongoDB

Elasticsearch

Azure

Application Insights

Email

Rolling File
```

---

## Rolling File

```csharp
rollingInterval:
RollingInterval.Day
```

Options

```
Infinite

Year

Month

Day

Hour

Minute
```

---

## File Size Limit

```csharp
fileSizeLimitBytes:
10485760
```

10 MB

---

## Retain Files

```csharp
retainedFileCountLimit:30
```

Keep last 30 log files.

---

## JSON Logs

```csharp
.WriteTo.File(
    new JsonFormatter(),
    "Logs/log.json")
```

---

# NLog

Older but still popular.

Install

```bash
dotnet add package NLog.Web.AspNetCore
```

Configuration

```
NLog.config
```

Targets

```
File

Console

Database

Mail

Network
```

Example

```xml
<target
name="logfile"
type="File"
fileName="Logs/app.log"/>
```

---

# log4net

Apache logging framework.

Install

```bash
dotnet add package log4net
```

Configuration

```
log4net.config
```

Supports

```
File

Rolling File

Console

SMTP

Database
```

---

# Comparison

| Feature | Built-in | Serilog | NLog | log4net |
|----------|----------|----------|-------|----------|
| Console | ✅ | ✅ | ✅ | ✅ |
| File | ❌ | ✅ | ✅ | ✅ |
| Rolling File | ❌ | ✅ | ✅ | ✅ |
| JSON | ❌ | ✅ | Limited | ❌ |
| SQL | ❌ | ✅ | ✅ | ✅ |
| Seq | ❌ | ✅ | ❌ | ❌ |
| Elasticsearch | ❌ | ✅ | Plugin | Plugin |
| Structured Logging | Limited | ✅ | Partial | ❌ |
| Production | Basic | ⭐⭐⭐⭐⭐ | ⭐⭐⭐⭐ | ⭐⭐⭐ |

---

# Best Practices

✅ Use `ILogger<T>`

✅ Use structured logging

```csharp
logger.LogInformation(
    "Employee {Id}",
    id);
```

❌ Avoid

```csharp
logger.LogInformation(
    "Employee "+id);
```

---

✅ Log Exceptions

```csharp
logger.LogError(ex,
    "Database Error");
```

---

✅ Keep Information logs minimal.

---

✅ Use Warning for recoverable issues.

---

✅ Use Error only for failures.

---

✅ Use Critical only when application cannot continue.

---

✅ Use Serilog for production.

---

# Interview Questions

- What is ILogger?
- What is a logging provider?
- Difference between Console and Debug logging?
- What is structured logging?
- What is Serilog?
- What is NLog?
- What is log4net?
- What is rolling file logging?
- What is MinimumLevel?
- Difference between Error and Critical?
- Why use placeholders (`{Id}`) instead of string concatenation?
- What is EventId?
- What is BeginScope()?
- Why use file logging in production?
- Difference between built-in logging and Serilog?

---

# Summary

- `ILogger<T>` is the logging interface.
- Providers determine where logs are written.
- Built-in providers include Console, Debug, EventLog, and EventSource.
- Built-in logging does **not** support file logging.
- **Serilog** is the recommended library for production due to structured logging and extensive sink support.
- **NLog** is a mature alternative with XML-based configuration.
- **log4net** is an older, stable framework still used in legacy projects.
- Prefer structured logging, appropriate log levels, and centralized file or external log storage for production applications.