# LOGS

### 1. What Is Logging?
- Logging means recording information about what your application is doing.

**Example:**
- 2026-08-22 01:30:10 INF Application started
- 2026-08-22 01:30:15 INF Employee API called
- 2026-08-22 01:30:16 INF Employee 101 created
- 2026-08-22 01:30:20 WRN External API response was slow
- 2026-08-22 01:30:25 ERR Database operation failed

**Logs help you answer:**
- What happened?
- When did it happen?
- Where did it happen?
- Which user/request caused it?
- Why did it fail?
- How long did it take?
- Which server/application processed it?


### 4. .NET Logging Architecture

The most important architecture to understand is:
```
Your Application Code
        |
        v
     ILogger
        |
        v
 Logging Infrastructure
        |
        +------------------+
        |                  |
        v                  v
   Provider/Sink       Configuration
        |
        v
    Formatter
        |
        v
    Destination
```

### Possible destinations:
- Console
- File
- Windows Event Log
- Database
- Seq
- Elasticsearch
- Application Insights
- Cloud logging
- Loki
etc.



### The Important Interfaces: .NET logging mainly revolves around:
- ILogger
- ILogger<T>
- ILoggerFactory
- ILoggerProvider

**And a concrete implementation:**
- LoggerFactory


## .NET Logging — ILogger and ILogger<T>

### 1. ILogger — Non-Generic
- ILogger is the non-generic logging interface.

```cs
ILogger logger;
```

**You normally get it using ILoggerFactory:**
```cs
ILogger logger = loggerFactory.CreateLogger("EmployeeService");
logger.LogInformation("Employee created");
```

**Here you manually provide the category:** Category = EmployeeService

**Simple flow:**
```
ILoggerFactory
      ↓
CreateLogger("EmployeeService")
      ↓
   ILogger
      ↓
LogInformation()
```

### 2. ILogger<T> — Generic
- ILogger<T> is the generic version of ILogger.

```cs
ILogger<EmployeeService> logger;
```
Here: T = EmployeeService

- .NET automatically uses the type as the logging category.

Example:
```cs
public class EmployeeService
{
    private readonly ILogger<EmployeeService> _logger;
    public EmployeeService(ILogger<EmployeeService> logger)
    {
        _logger = logger;
    }
    public void CreateEmployee()
    {
        _logger.LogInformation("Employee created");
    }
}
```
Category: EmployeeService -> Based on T, because Dependency Injection automatically provides the correctly categorized logger.

**Simple flow:**
```
Dependency Injection
       ↓
ILogger<EmployeeService>
       ↓
T = EmployeeService
       ↓
Category = EmployeeService
```

3. `ILogger` vs `ILogger<T>`

|ILogger|ILogger`<T>`|
|------|-----|
|Non-generic|Generic|
|No <T>	|Has <T>|
Category usually specified | manually	Category based on T
ILogger logger |	ILogger<EmployeeService> logger
CreateLogger("EmployeeService")	|`CreateLogger<EmployeeService>()`
Less common in normal services |	Most commonly used


### 9. ILoggerFactory

- ILoggerFactory is used to create ILogger instances.

Example:
```cs
ILoggerFactory factory = ...;
ILogger logger = factory.CreateLogger<EmployeeService>();
```
or:
```cs
ILogger logger = factory.CreateLogger("EmployeeService");
```
Think:
```
ILoggerFactory
       |
       +---- CreateLogger()
       |
       +---- CreateLogger<T>()
```


If you mean what difference will actually appear in the log file between ILogger and ILogger<T>, the main difference is the category/source name.

#### 1. Using ILogger
```cs
ILogger logger = loggerFactory.CreateLogger("EmployeeService");
logger.LogInformation("Employee created");
```
Log file might show:
```
2026-08-22 02:00:00 [INF] EmployeeService: Employee created
```
Here you manually gave:

Category = EmployeeService


#### 2. Using ILogger<EmployeeService>
```cs
ILogger<EmployeeService> logger;
logger.LogInformation("Employee created");
```
Log file might show:
```
2026-08-22 02:00:00 [INF] EmployeeService: Employee created
```
Here .NET gets the category from: T = EmployeeService

So the log message itself is usually the same Employee created

**The important difference is how the category is obtained:**
```
ILogger
   ↓
You specify category
   ↓
EmployeeService
```
```
ILogger<EmployeeService>
   ↓
T = EmployeeService
   ↓
Category automatically comes from T
```


#### Example with different categories
With non generic loggers:
```cs
ILogger employeeLogger = factory.CreateLogger("EmployeeService");
ILogger paymentLogger = factory.CreateLogger("PaymentService");
```
**Log:**
```
[INF] EmployeeService: Employee created
[INF] PaymentService: Payment completed
```
With generic loggers:
```cs
ILogger<EmployeeService>
ILogger<PaymentService>
```
**you get the equivalent categories automatically:**

[INF] EmployeeService: Employee created
[INF] PaymentService: Payment completed

**Important:** the exact text format depends on the logging provider/formatter. ILogger vs `ILogger<T>` does not itself decide the log-file format.

#### 10. ILoggerFactory vs ILogger

Very important:

ILogger = "I want to write logs."
ILoggerFactory = "I want to create/get a logger."

Example:
```cs
ILoggerFactory factory;
```
creates:
```cs
ILogger logger;
```


## 11. LoggerFactory

LoggerFactory is a concrete implementation of: ILoggerFactory

So:
```
ILoggerFactory
     ↑
     |
LoggerFactory
```
ILoggerFactory is the interface.

LoggerFactory is a concrete class implementing that interface.

⸻

**LoggerFactory Example:**

You can manually create a factory:
```cs
using Microsoft.Extensions.Logging;
using ILoggerFactory factory =LoggerFactory.Create(builder =>
    {
        builder.AddConsole();
    });
ILogger logger = factory.CreateLogger("MyApplication");
logger.LogInformation("Application started");
```
Conceptually:
```
LoggerFactory
      |
      v
CreateLogger("MyApplication")
      |
      v
   ILogger
      |
      v
LogInformation()
      |
      v
    Console
```
⸻

13. Why Don’t We Normally Create LoggerFactory Manually?

In ASP.NET Core/.NET applications, the Dependency Injection container creates and manages the logging infrastructure.

You normally do:
```cs
private readonly ILogger<EmployeeService> _logger;
public EmployeeService(ILogger<EmployeeService> logger)
{
    _logger = logger;
}
```
You don’t normally do:

new LoggerFactory(...)

inside every service.

⸻

14. What Happens Internally?

Suppose you write:
```cs
_logger.LogInformation("Employee {EmployeeId} created", employeeId);
```
Conceptually:
```
Your Service
     |
     v
ILogger<EmployeeService>
     |
     v
Logging infrastructure
     |
     v
Check log level
     |
     v
Create/process log event
     |
     v
Providers
     |
     +------> Console
     |
     +------> File
     |
     +------> EventLog
     |
     +------> Cloud
```
You only interact with:

ILogger

⸻

## 15. ILoggerProvider

A provider connects the .NET logging abstraction to a destination/system.

Conceptually:
```
ILogger
   |
   v
ILoggerProvider
   |
   v
Destination
```

Examples:
- Console provider
- Debug provider
- EventLog provider
- Third-party provider

⸻

16. Provider vs Destination

Don’t confuse them.

For example:
```
ILogger
   ↓
ConsoleLoggerProvider
   ↓
Console
```
The provider creates/manages the logger that writes to the destination.

Another example:

ILogger
   ↓
EventLogLoggerProvider
   ↓
Windows Event Viewer

⸻

#### 17. Built-in .NET Logging

.NET provides logging abstractions and common providers.

**Typical providers include:**
- Console
- Debug
- EventSource
- EventLog

Third-party frameworks can provide additional destinations.

⸻

18. Basic Program.cs

For an ASP.NET Core application:

var builder = WebApplication.CreateBuilder(args);
builder.Logging.AddConsole();
builder.Logging.AddDebug();
var app = builder.Build();
app.Run();

Now application code can use:

ILogger<T>

⸻

#### 19. ClearProviders()

You may see:
```cs
builder.Logging.ClearProviders();
```
This removes currently configured logging providers.

Then:
```cs
builder.Logging.AddConsole();
```
adds Console logging.

Example:
```cs
var builder = WebApplication.CreateBuilder(args);
builder.Logging.ClearProviders();
builder.Logging.AddConsole();
var app = builder.Build();
app.Run();
```

**Architecture:**
```
Default Providers
      |
      X
ClearProviders()
      |
      v
No providers
      |
      v
AddConsole()
      |
      v
Console provider
```

## 20. Log Levels

.NET has these main levels:
- Trace
- Debug
- Information
- Warning
- Error
- Critical

**In increasing severity:**
```
Trace
 ↓
Debug
 ↓
Information
 ↓
Warning
 ↓
Error
 ↓
Critical
```

### 21. Trace

Extremely detailed information.
```cs
_logger.LogTrace("Entering method GetEmployee");
```
- Usually used temporarily or for very detailed diagnostics.


### 22. Debug

Developer-oriented diagnostic information.
```cs
_logger.LogDebug("Employee query parameter is {EmployeeId}", employeeId);
```
Usually enabled during development/troubleshooting.



### 23. Information

Normal application events.
```cs
_logger.LogInformation("Employee {EmployeeId} created", employeeId);
```
**Examples:**
- Application started
- Application stopped
- Job completed
- Employee created
- Payment completed


### 24. Warning
Something unexpected happened, but the application can continue.

```cs
_logger.LogWarning("Payment API response took {ElapsedMs} ms", elapsedMs);
```
**Examples:**
- Retry required
- Slow external service
- Configuration fallback used
- Approaching resource limit


### 25. Error

An operation failed.
```cs
_logger.LogError(ex, "Failed to create employee {EmployeeId}", employeeId);
```
**Examples:**
- Database query failed
- External API failed
- File processing failed


### 26. Critical

Very serious failure.
```cs
_logger.LogCritical(ex, "Application cannot connect to required database");
```
**Examples:**
- Application cannot start
- Required infrastructure unavailable
- Critical service failure


## 27. Minimum Log Level
**Suppose configuration says:** `Information`

Then:
```
Trace        ❌
Debug        ❌
Information  ✅
Warning      ✅
Error        ✅
Critical     ✅
```
**If configured as:** `Warning`

then:
```
Trace        ❌
Debug        ❌
Information  ❌
Warning      ✅
Error        ✅
Critical     ✅
```


## 28. appsettings.json Logging

**Built-in configuration:**
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.AspNetCore": "Warning"
    }
  }
}
```
**Meaning:**
- Your application: Information+
- Microsoft: Warning+
- Microsoft.AspNetCore: Warning+


### 29. Why Microsoft Logs Are Often Warning

- ASP.NET Core and other framework components can generate a lot of logs.
- If you use: "Microsoft": "Information": you may receive a large amount of framework logging.
- Therefore production commonly uses: "Microsoft": "Warning"
- while application logs remain: Information


30. Logging Category

Suppose: `ILogger<EmployeeService>`

Category: EmployeeService

Suppose: `ILogger<EmployeeController>`

Category: EmployeeController

**You can configure categories independently:**
Example:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "MyApp.Services.EmployeeService": "Debug",
      "Microsoft": "Warning"
    }
  }
}
```

### 31. Logging a Variable

Recommended:
```cs
_logger.LogInformation("Employee {EmployeeId} created", employeeId);
```
Don’t normally do:
```cs
_logger.LogInformation("Employee " + employeeId + " created");
```
- The first approach is structured logging.


#### 32. Structured Logging

This:
```cs
_logger.LogInformation("Employee {EmployeeId} created", employeeId);
```
has:
Message template: Employee {EmployeeId} created

Property:EmployeeId = 101

The logging system can preserve: EmployeeId = 101 as structured data.


#### 33. Multiple Structured Properties
```cs
_logger.LogInformation("Employee {EmployeeId} created by {UserId} in {Department}", employeeId, userId, department);
```

Possible structured event:
```cs
{
  "Message": "Employee 101 created by 500 in IT",
  "EmployeeId": 101,
  "UserId": 500,
  "Department": "IT"
}
```

### 34. Exception Logging

Best:
```cs
try
{
    await service.CreateEmployee();
}
catch (Exception ex)
{
    _logger.LogError(ex, "Employee creation failed");
}
```
Notice:
```cs
_logger.LogError(ex, "...");
```
The exception is passed separately.

This allows logging systems to preserve:

- Exception type
- Message
- Stack trace
- Inner exception


#### 35. Bad Exception Logging

Avoid:
```cs
_logger.LogError(ex.Message);
```
- You lose the full exception context.

Avoid:
```cs
_logger.LogError(ex.ToString());
```
- when structured exception handling is available.

Prefer:
```cs
_logger.LogError(ex, "Employee creation failed for {EmployeeId}", employeeId);
```


## 36. ILoggerFactory CreateLogger

You can create a logger from a category string:
```cs
ILogger logger = loggerFactory.CreateLogger("EmployeeService");
```
**Or:**
```cs
ILogger<EmployeeService> logger = loggerFactory.CreateLogger<EmployeeService>();
```
The factory knows which logging providers/configuration are available.


37. Why CreateLogger() Is Useful

Instead of:
```cs
loggerFactory.CreateLogger(typeof(EmployeeService).FullName);
```
you can do:
```cs
loggerFactory.CreateLogger<EmployeeService>();
```
Cleaner and type-safe.


38. ILoggerFactory in Dependency Injection

You can inject:
```cs
public class EmployeeService
{
    private readonly ILogger<EmployeeService> _logger;
    public EmployeeService(ILogger<EmployeeService> logger)
    {
        _logger = logger;
    }
}
```
You can also inject:
```cs
public class SomeService
{
    private readonly ILoggerFactory _loggerFactory;
    public SomeService(ILoggerFactory loggerFactory)
    {
        _loggerFactory = loggerFactory;
    }
}
```
Then:
```cs
var logger = _loggerFactory.CreateLogger("DynamicCategory");
```
This is useful when the category must be dynamically selected.

But for normal services, prefer ILogger<T>.


39. LoggerFactory Lifetime

In a normal .NET application’s DI logging infrastructure, the factory is managed by the framework/container.

You should not create a new LoggerFactory for every log message.

Bad:
```cs
public void DoSomething()
{
    using var factory = LoggerFactory.Create(builder => builder.AddConsole());
    var logger = factory.CreateLogger("Test");
    logger.LogInformation("Hello");
}
```
Doing this repeatedly creates unnecessary logging infrastructure.

Prefer dependency injection.

⸻

### 40. ILogger Lifetime

`You normally don’t manually manage an injected ILogger<T>.`

Example:
```cs
private readonly ILogger<EmployeeService> _logger;
```
The .NET logging infrastructure manages the underlying logging system.

Do not do:
```cs
_logger.Dispose();
```
for the injected logger.

⸻

41. LoggerFactory vs Logger

Think of it like this:
```
LoggerFactory
     |
     | CreateLogger()
     v
ILogger
     |
     | LogInformation()
     v
Log Event
```
So:

Factory = creates logger
Logger = writes log
Provider = handles destination

This three-part mental model is extremely important.

⸻

42. Logging Provider Architecture

Conceptually:
```
                  ILoggerFactory
                        |
            +-----------+-----------+
            |           |           |
            v           v           v
       Console       Debug       EventLog
       Provider      Provider     Provider
            |           |           |
            v           v           v
         Console       IDE       Event Viewer
```
One ILogger can send the event through multiple configured providers.

⸻

### 43. Multiple Providers

Example:
```cs
builder.Logging.ClearProviders();
builder.Logging.AddConsole();
builder.Logging.AddDebug();
```
A log:
```cs
_logger.LogInformation("Application started");
```
can go to:

Console
+
Debug output

⸻

## 44. File Logging

- Built-in ILogger abstraction doesn’t mean your logs automatically go to: app.log

- You need a file-capable provider/framework. A popular approach is: `Serilog`



### 45. Serilog

Serilog is a popular structured logging framework.

Architecture:
```
Application
     |
     v
  ILogger
     |
     v
  Serilog
     |
     +---- Console
     |
     +---- File
     |
     +---- Seq
     |
     +---- Elasticsearch
     |
     +---- Database
```
⸻

46. Why Use Serilog?

Serilog gives you:

File logging
Rolling files
JSON logs
Structured properties
Filtering
Enrichment
Multiple destinations
Centralized logging integrations

⸻

47. Basic Serilog Setup

Typical packages:
```bash
dotnet add package Serilog.AspNetCore
dotnet add package Serilog.Sinks.File
```

Then:
```cs
using Serilog;
var builder = WebApplication.CreateBuilder(args);
Log.Logger = new LoggerConfiguration()
    .WriteTo.Console()
    .WriteTo.File("_Logs/app.log")
    .CreateLogger();
builder.Host.UseSerilog();
var app = builder.Build();
app.Run();
```
⸻

#### 48. Serilog Rolling File

Instead of one huge file:
```cs
.WriteTo.File(
    "_Logs/app-.log",
    rollingInterval: RollingInterval.Day)
```
Possible result:
```
logs/
    app-2026-08-20.log
    app-2026-08-21.log
    app-2026-08-22.log
```
⸻

49. Size-Based Rolling

- You can also roll when the file becomes too large.

Concept:
```cs
.WriteTo.File(
    "_Logs/app-.log",
    rollingInterval: RollingInterval.Day,
    fileSizeLimitBytes: 10_000_000,
    rollOnFileSizeLimit: true)
```
Now both time and file size can be considered.

⸻

#### 50. Retention

Example:
```cs
.WriteTo.File(
    "_Logs/app-.log",
    rollingInterval: RollingInterval.Day,
    retainedFileCountLimit: 30)
```
This prevents unlimited historical files from accumulating.


### 51. Serilog Minimum Level
```cs
Log.Logger = new LoggerConfiguration()
    .MinimumLevel.Information()
    .WriteTo.Console()
    .WriteTo.File("_Logs/app.log")
    .CreateLogger();
```
**Then:**
- Trace        ❌
- Debug        ❌
- Information  ✅
- Warning      ✅
- Error        ✅
- Critical     ✅


### 52. Serilog appsettings Configuration

You can put Serilog configuration in: `appsettings.json`

Example:
```json
{
  "Serilog": {
    "MinimumLevel": {
      "Default": "Information",
      "Override": {
        "Microsoft": "Warning",
        "Microsoft.AspNetCore": "Warning"
      }
    },
    "WriteTo": [
      {
        "Name": "Console"
      },
      {
        "Name": "File",
        "Args": {
          "path": "logs/app-.log",
          "rollingInterval": "Day"
        }
      }
    ]
  }
}
```

53. appsettings vs Program.cs

You can configure logging in:

Program.cs

or:

appsettings.json

or a combination.

Configuration files are especially useful because you can change operational settings without changing application code.

⸻

54. Development and Production Logging

Typical files:

- appsettings.json
- appsettings.Development.json
- appsettings.Production.json

Development:

{
  "Logging": {
    "LogLevel": {
      "Default": "Debug"
    }
  }
}

Production:

{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning"
    }
  }
}

⸻

55. Logging Scope

A scope adds contextual information to multiple logs.

Example:
```cs
using (_logger.BeginScope(new Dictionary<string, object>
    {
        ["RequestId"] = requestId,
        ["UserId"] = userId
    }))
{
    _logger.LogInformation("Request started");
    _logger.LogInformation("Database operation started");
    _logger.LogInformation("Request completed");
}
```
Conceptually:

RequestId = ABC123
UserId = 500
    Request started
    Database operation started
    Request completed

⸻

56. Why Scopes Are Useful

Imagine:
```
Request
 ↓
Controller
 ↓
Service
 ↓
Repository
 ↓
Database
```
You want all logs to contain:

RequestId = ABC123

A scope can carry this contextual information.

⸻

57. Correlation ID

A correlation ID allows you to connect logs for one business/request flow.

Example:

CorrelationId = 7f9c123

Logs:

Request received       7f9c123
Authentication         7f9c123
Employee service       7f9c123
Database query         7f9c123
External API           7f9c123
Response returned      7f9c123

Now you can search:

CorrelationId = 7f9c123

and find the entire flow.

⸻

58. Distributed Systems

Suppose:

Frontend
   ↓
API Gateway
   ↓
Employee API
   ↓
Payment Service
   ↓
Notification Service

A correlation ID can travel through the services.

CorrelationId = ABC123

Then:

Gateway           ABC123
Employee API      ABC123
Payment Service   ABC123
Notification      ABC123

This is extremely useful in microservices.

⸻

59. HTTP Request Logging

You may want to record:

HTTP method
URL
Status code
Duration
Request ID
Correlation ID

Example:

GET /api/employees
Status = 200
Duration = 35ms

With Serilog ASP.NET Core integration, request logging can be enabled with:

app.UseSerilogRequestLogging();

⸻

60. Custom Request Logging Middleware

Example:
```cs
public class RequestLoggingMiddleware
{
    private readonly RequestDelegate _next;
    private readonly ILogger<RequestLoggingMiddleware> _logger;
    public RequestLoggingMiddleware(RequestDelegate next,ILogger<RequestLoggingMiddleware> logger)
    {
        _next = next;
        _logger = logger;
    }
    public async Task InvokeAsync(HttpContext context)
    {
        var stopwatch = Stopwatch.StartNew();
        _logger.LogInformation("Request {Method} {Path} started", context.Request.Method, context.Request.Path);

        await _next(context);
        stopwatch.Stop();
        _logger.LogInformation("Request {Method} {Path} returned {StatusCode} in {ElapsedMs} ms",
            context.Request.Method,
            context.Request.Path,
            context.Response.StatusCode,
            stopwatch.ElapsedMilliseconds);
    }
}
```
Register:
```cs
app.UseMiddleware<RequestLoggingMiddleware>();
```
⸻

### 61. Global Exception Logging

Instead of putting:

try/catch

in every controller, use centralized exception handling.

Conceptually:

HTTP Request
     ↓
Middleware
     ↓
Controller
     ↓
Service
     ↓
Repository
     ↓
Exception
     ↓
Global Exception Handler
     ↓
ILogger
     ↓
Log storage

This gives consistent error handling.

⸻

62. Don’t Log the Same Exception Everywhere

Bad:

Repository → ERROR
Service    → ERROR
Controller → ERROR
Middleware → ERROR

The same exception could appear four times.

Better:

Repository
   ↓
throw
   ↓
Service
   ↓
throw
   ↓
Global Handler
   ↓
Log once with useful context

Of course, if a lower layer adds unique diagnostic context that would otherwise be lost, selective logging can still be appropriate.

⸻

63. BackgroundService Logging

Example:
```cs
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;
    public Worker(ILogger<Worker> logger)
    {
        _logger = logger;
    }
    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogInformation("Worker started");
        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogInformation("Worker processing started");
            try
            {
                // background work
            }
            catch (Exception ex)
            {
                _logger.LogError(ex, "Background processing failed");
            }
            await Task.Delay(TimeSpan.FromMinutes(1), stoppingToken);
        }
        _logger.LogInformation("Worker stopped");
    }
}
```
⸻

64. BackgroundService + Database

If your worker uses EF Core:
```
BackgroundService
      ↓
ILogger<Worker>
      ↓
Service
      ↓
DbContext
```
You can log:
```cs
_logger.LogInformation("Starting database processing");
```
and:
```cs
_logger.LogError(ex, "Database processing failed");
```
Remember that DbContext itself normally has a scoped lifetime, so background services often create a scope before resolving it.

⸻

65. Logging Database Operations

Good:
```cs
_logger.LogInformation("Fetching employee {EmployeeId}", employeeId);
```
Bad:
```cs
_logger.LogInformation("SQL: {Sql}", sql);
```
especially when SQL or parameters may contain sensitive data.

⸻

66. EF Core Logging

You can configure EF Core categories.

Example:
```json
{
  "Logging": {
    "LogLevel": {
      "Microsoft.EntityFrameworkCore": "Warning"
    }
  }
}
```
For temporary troubleshooting, a more detailed category may be enabled.

But production SQL logging should be used carefully because it can generate high volume and potentially expose sensitive values.

⸻

67. Audit Logging

Audit logging answers:

WHO?
WHAT?
WHEN?
WHERE?
RESULT?

Example:
```json
{
  "UserId": 500,
  "Action": "EmployeeSalaryChanged",
  "EmployeeId": 101,
  "Timestamp": "2026-08-22T01:40:00",
  "Result": "Success"
}
```
Normal application log:

Employee API called

Audit log:

User 500 changed employee 101 salary

These are not the same thing.

⸻

68. Security Logging

Useful events:

Login success
Login failure
Logout
Account locked
Permission denied
Role changed
Token validation failure
Suspicious request

Example:
```cs
_logger.LogWarning("Login failed for user {UserId}", userId);
```
⸻

69. Never Log Secrets

Never log:

Password
OTP
JWT
Refresh token
API key
Private key
Database password
Encryption key
Credit card information

Bad:
```cs
_logger.LogInformation("Token: {Token}", token);
```
Bad:
```cs
_logger.LogInformation("Password: {Password}", password);
```
Bad:
```cs
_logger.LogInformation("PrivateKey: {PrivateKey}", privateKey);
```
Logs themselves can become a security risk.

⸻

70. Logging Request Bodies

Avoid:
```cs
_logger.LogInformation("Request body: {@Request}", request);
```
because the object may contain sensitive information.

Prefer:
```cs
_logger.LogInformation("Create employee request received for {EmployeeId}", request.EmployeeId);
```
Log only what is needed.

⸻

71. JSON Logging

Modern systems often prefer structured JSON.

Example:
```json
{
  "Timestamp": "2026-08-22T01:45:00Z",
  "Level": "Information",
  "Message": "Employee 101 created",
  "EmployeeId": 101,
  "Application": "EmployeeAPI",
  "Environment": "Production",
  "Machine": "SERVER01"
}
```
Advantages:

Easy searching
Easy filtering
Machine readable
Centralized logging friendly
Cloud friendly

⸻

72. Text vs JSON

Text

2026-08-22 INF Employee 101 created

Good for:

Human reading
Simple local logs

```JSON
{
  "Level": "Information",
  "EmployeeId": 101
}
```
Good for:

ELK
Seq
Cloud
Loki
Analytics
Automated searching

⸻

73. Log Enrichment

Enrichment means adding common properties automatically.

For example:

Application = EmployeeAPI
Environment = Production
MachineName = SERVER01
Version = 2.5.0

Then every log contains these values.

Example:
```json
{
  "Application": "EmployeeAPI",
  "Environment": "Production",
  "Version": "2.5.0",
  "Message": "Employee created"
}
```
⸻

74. Machine Name

Useful in multi-server deployments.

SERVER01
SERVER02
SERVER03

Suppose an error occurs:

MachineName = SERVER02

Now you know where it happened.

⸻

75. Application Name

If multiple applications send logs to the same system:

EmployeeAPI
PaymentAPI
NotificationAPI
AuthAPI

You can filter:

Application = PaymentAPI

⸻

76. Environment

Useful values:

Development
Test
Staging
Production

Example:

Environment = Production

This prevents confusion when all environments send logs to a central system.

⸻

77. Version Logging

Example:

ApplicationVersion = 2.5.1

Suppose errors suddenly increase after deployment.

You can search:

Version = 2.5.1

and identify whether the new version caused the problem.

⸻

78. Performance Logging

You can manually measure execution time:
```cs
var stopwatch = Stopwatch.StartNew();
await ProcessEmployee();
stopwatch.Stop();
_logger.LogInformation("Employee processing completed in {ElapsedMs} ms", stopwatch.ElapsedMilliseconds);
```
Useful for:

API
Database
External service
Background job
File processing

⸻

79. Metrics vs Logs

Don’t use logs for everything.

Log

Payment failed for Order 1001

Metric

Payment failure count = 1,523

Metrics are better for:

CPU
Memory
Request count
Error rate
Latency
Throughput

⸻

80. Tracing

Tracing follows a request through the system.

Example:
```
Request
   |
   +-- API 20ms
   |
   +-- Database 100ms
   |
   +-- External API 300ms
```
You can discover:

Where is the request slow?
Which service failed?
Which database call is expensive?

⸻

81. Logs + Metrics + Traces

Modern observability uses all three:
```
              Observability
                    |
        +-----------+-----------+
        |           |           |
       Logs       Metrics      Traces
        |           |           |
     Events      Numbers     Request flow
```
⸻

82. OpenTelemetry

OpenTelemetry provides a standardized approach to collecting telemetry.

It can work with:

Logs
Metrics
Traces

Architecture:

.NET Application
       |
       +---- Logs
       |
       +---- Metrics
       |
       +---- Traces
                |
                v
          OpenTelemetry
                |
                v
       Observability Backend

⸻

83. Centralized Logging

Suppose you have:

Server 1
Server 2
Server 3
Server 4

Each produces:

app.log

Searching manually is difficult.

Instead:

Server 1 ─┐
Server 2 ─┤
Server 3 ─┼──> Central Logging
Server 4 ─┘

Then search all logs from one place.

⸻

84. Common Centralized Logging Systems

Examples:

Elasticsearch + Kibana
Seq
Grafana Loki
Splunk
Azure Application Insights
AWS CloudWatch
Google Cloud Logging

⸻

85. Elasticsearch Architecture

A common architecture:
```
.NET
 ↓
Serilog
 ↓
Elasticsearch
 ↓
Kibana
```
Kibana can provide:

Search
Filtering
Dashboards
Charts
Alerts

⸻

86. Loki Architecture

Another approach:
```
.NET
 ↓
Logging agent / collector
 ↓
Loki
 ↓
Grafana
```
Useful for centralized log aggregation and visualization.

⸻

87. Windows Event Log

On Windows applications/services:

.NET
 ↓
ILogger
 ↓
Windows Event Log
 ↓
Event Viewer

Useful for:

Windows Services
Enterprise applications
Windows infrastructure

⸻

88. IIS Logs vs .NET Logs

These are different.

IIS

Records web-server information:

IP
URL
HTTP method
Status code
Request

.NET application

Records:

Business logic
Database errors
Application events
Exceptions
User operations

You may need both.

Architecture:

Browser
   ↓
IIS
   ↓
ASP.NET Core
   ↓
Application

Therefore:

IIS logs
+
Application logs

provide a better picture.

⸻

89. File Logging in IIS

Suppose your application writes:

C:\MyApp\logs\app.log

The process identity needs permission to write there.

If it doesn’t:

Access denied

You need to configure appropriate Windows filesystem permissions for the identity running the IIS application pool.

⸻

90. Log Rotation

Never allow production logs to grow forever.

Example:

app-2026-08-20.log
app-2026-08-21.log
app-2026-08-22.log

Possible rotation strategies:

Daily
Hourly
Size-based
Daily + size-based

⸻

91. Log Retention

Retention means how long logs are kept.

Example:

7 days
30 days
90 days
1 year

It depends on:

Storage
Security
Compliance
Business requirements
Troubleshooting requirements

⸻

92. Separate Log Files

You can conceptually have:

logs/
    application.log
    error.log
    audit.log
    security.log

For example:

Application

Information
Warning

Error

Error
Critical

Audit

User actions
Business actions

Security

Login
Authorization
Suspicious activity

The actual configuration depends on the logging framework.

⸻

93. Database Logging

You can store logs in a database:

Application
    ↓
ILogger
    ↓
Logging Framework
    ↓
Database

Example table:

ApplicationLogs
--------------------------------
Id
Timestamp
Level
Category
Message
Exception
UserId
CorrelationId
MachineName
Application

Advantages:

SQL search
Central storage
Reporting

Disadvantages:

Database load
Storage growth
Database may itself be unavailable
High-volume logs can become expensive

For very high-volume logging, specialized log stores are often more appropriate.

⸻

94. Multiple Destinations

You can send one event to multiple places:

                Console
                   ↑
                   |
Application → Serilog
                   |
            +------+------+
            |             |
            v             v
          File         Central Log

For example:

Production:
Console + centralized logging
Small internal application:
Console + rolling file

⸻

95. Custom File Logger

You can build your own:

ILoggerProvider
      ↓
CustomLogger
      ↓
FileWriter

You would typically implement:

ILogger
ILoggerProvider

and possibly custom formatting/configuration.

However, building your own logger is usually unnecessary when mature frameworks already solve the problem.

⸻

96. Why Not Use File.WriteAllText?

You could technically do:

File.AppendAllText(
    "app.log",
    "Application started");

But this is not a proper application logging architecture.

Problems include:

Concurrency
Formatting
Log levels
Filtering
Rotation
Retention
Structured data
Performance
Multiple destinations
Exception handling

Use ILogger and a proper logging provider/framework instead.

⸻

97. LoggerFactory vs File.Write

Correct architecture:

Application
   ↓
ILogger
   ↓
ILoggerFactory
   ↓
Provider
   ↓
File

Not:

Application
   ↓
File.AppendAllText()

for general application logging.

⸻

98. LoggerFactory and Providers

The factory manages the logging infrastructure.

Conceptually:

LoggerFactory
    |
    +---- Console Provider
    |
    +---- Debug Provider
    |
    +---- EventLog Provider

When you call:

factory.CreateLogger<EmployeeService>();

you get a logger associated with the category.

⸻

99. LoggerFactory and Multiple Loggers

One factory can create multiple category loggers:

var employeeLogger =
    factory.CreateLogger<EmployeeService>();
var paymentLogger =
    factory.CreateLogger<PaymentService>();
var authLogger =
    factory.CreateLogger<AuthService>();

Conceptually:

                 LoggerFactory
                      |
          +-----------+-----------+
          |           |           |
          v           v           v
    EmployeeLogger PaymentLogger AuthLogger

All use the same logging infrastructure.

⸻

100. Don’t Create Factory Per Class Manually

Avoid:

var factory = LoggerFactory.Create(...);

inside every class.

Instead:

ILogger<EmployeeService>

through DI.

The framework manages the common logging infrastructure.

⸻

101. LoggerMessage

For high-performance logging, .NET provides LoggerMessage.

Example:

private static readonly Action<
    ILogger,
    int,
    Exception?> EmployeeCreated =
    LoggerMessage.Define<int>(
        LogLevel.Information,
        new EventId(1001, "EmployeeCreated"),
        "Employee {EmployeeId} created");

Then:

EmployeeCreated(
    _logger,
    employeeId,
    null);

This can reduce overhead in very high-volume logging.

⸻

102. Source-Generated Logging

Modern .NET also supports source-generated logging.

Example:

public static partial class LogMessages
{
    [LoggerMessage(
        EventId = 1001,
        Level = LogLevel.Information,
        Message = "Employee {EmployeeId} created")]
    public static partial void EmployeeCreated(
        ILogger logger,
        int employeeId);
}

Use:

LogMessages.EmployeeCreated(
    _logger,
    employeeId);

This is useful for high-performance applications.

⸻

103. Event ID

Logs can have event IDs:

_logger.LogInformation(
    new EventId(1001, "EmployeeCreated"),
    "Employee {EmployeeId} created",
    employeeId);

Example event catalog:

1001 EmployeeCreated
1002 EmployeeUpdated
1003 EmployeeDeleted
2001 PaymentCreated
2002 PaymentFailed
3001 LoginFailed

This can make filtering and monitoring easier.

⸻

104. Logging Categories + Event IDs

You can think of an event as:

Category
+
Level
+
EventId
+
Message
+
Properties
+
Exception

Example:

Category: EmployeeService
Level: Error
EventId: 2001
EmployeeId: 101
Message: Employee creation failed
Exception: SqlException

⸻

105. Logging Performance

Logging itself has a cost.

Bad:
```cs
_logger.LogInformation("Large object: " + SerializeHugeObject());
```
The serialization may happen even if Information logging is disabled.

Better structured logging:
```cs
_logger.LogInformation("Employee {EmployeeId} created", employeeId);
```
For very high-performance logging, use:

LoggerMessage
Source-generated logging
Appropriate log levels

⸻

106. Check IsEnabled

For expensive operations:
```cs
if (_logger.IsEnabled(LogLevel.Debug))
{
    var expensiveData = BuildExpensiveDebugData();
    _logger.LogDebug("Debug data: {Data}", expensiveData);
}
```
This prevents expensive preparation when Debug logging isn’t enabled.

⸻

107. Logging Large Objects

Avoid:
```cs
_logger.LogInformation("{@HugeObject}", hugeObject);
```
if the object contains thousands of properties/records.

Instead:
```cs
_logger.LogInformation("Processed {RecordCount} records", records.Count);
```
Log meaningful summaries.

⸻

### 108. Logging in Controllers

Example:
```cs
[ApiController]
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
    private readonly ILogger<EmployeeController> _logger;
    public EmployeeController(ILogger<EmployeeController> logger)
    {
        _logger = logger;
    }
    [HttpGet("{id}")]
    public async Task<IActionResult> Get(int id)
    {
        _logger.LogInformation("Get employee request received for {EmployeeId}", id);
        // service call
        return Ok();
    }
}
```
⸻

109. Logging in Services
```cs
public class EmployeeService
{
    private readonly ILogger<EmployeeService> _logger;
    public EmployeeService(ILogger<EmployeeService> logger)
    {
        _logger = logger;
    }
    public async Task CreateEmployee()
    {
        _logger.LogInformation("Employee creation started");
        // business logic
        _logger.LogInformation("Employee creation completed");
    }
}
```
⸻

110. Logging in Repository
```cs
public class EmployeeRepository
{
    private readonly ILogger<EmployeeRepository> _logger;
    public EmployeeRepository(ILogger<EmployeeRepository> logger)
    {
        _logger = logger;
    }
    public async Task<Employee?> Get(int id)
    {
        _logger.LogDebug("Fetching employee {EmployeeId}", id);
        // database operation
        return null;
    }
}
```
⸻

111. Logging API Request Flow

A good API flow can look like:
```
Request
 ↓
Correlation ID
 ↓
Request logging
 ↓
Authentication
 ↓
Authorization
 ↓
Controller
 ↓
Service
 ↓
Repository
 ↓
Database
 ↓
Response
```
Logs might be:

INFO Request started
INFO Authentication successful
INFO Get employee 101
DEBUG Database query started
INFO Database query completed
INFO Response 200

⸻

112. Logging Background Job Flow
```
Worker started
      ↓
Job picked
      ↓
Job ID = 1001
      ↓
Database read
      ↓
Processing
      ↓
External API
      ↓
Job completed
```
Use:

JobId
CorrelationId

to connect the logs.

⸻

113. Logging Scheduled Jobs

Example:
```cs
_logger.LogInformation("Job {JobId} started", jobId);
```
Then:
```cs
_logger.LogInformation("Job {JobId} completed in {ElapsedMs} ms", jobId, elapsedMs);
```
Failure:
```cs
_logger.LogError(ex, "Job {JobId} failed", jobId);
```
⸻

114. Logging Retry Operations

Example:
```cs
_logger.LogWarning("External API attempt {Attempt} failed. Retrying...",attempt);
```
Don’t log every retry as Error if retrying is expected behavior.

Often:

Warning → retry
Error → final failure

is more meaningful.

⸻

115. Logging External APIs

Good:
```cs
_logger.LogInformation("Calling Payment API for Order {OrderId}", orderId);

After:

_logger.LogInformation("Payment API returned {StatusCode} for Order {OrderId}", statusCode, orderId);
```
Don’t log:

Authorization header
API key
JWT
Sensitive request body

⸻

116. Logging Configuration Errors

Example:
```cs
_logger.LogCritical("Required connection string 'DefaultConnection' is missing");
```
Application startup may fail if required configuration is missing.

⸻

117. Logging Environment

You can log:

Development
Staging
Production

Example:
```cs
_logger.LogInformation("Application started in {Environment}", environmentName);
```
Be careful not to expose secrets from configuration.

⸻

118. Logging Application Startup

Good startup logs:

Application starting
Environment = Production
Application version = 2.5.1
Database connectivity verified
Application started

Don’t log:

Database password
API key
Private key
JWT secret

⸻

119. Logging Shutdown

Useful:
```cs
_logger.LogInformation("Application shutting down");
```
For worker services:
```cs
_logger.LogInformation("Worker stopping");
```
⸻

120. Logging Configuration Changes

If configuration changes dynamically, you may want to log safe metadata:

Configuration reloaded
Configuration version changed
Feature flag changed

Don’t log secret values.

⸻

121. Log Filtering

Suppose you want:

MyApp → Debug
Microsoft → Warning
Microsoft.EntityFrameworkCore → Error

Configuration:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "MyApp": "Debug",
      "Microsoft": "Warning",
      "Microsoft.EntityFrameworkCore": "Error"
    }
  }
}
```
This is category-based filtering.

⸻

122. Filtering With Serilog

Serilog can also filter by:

Level
Category/SourceContext
Properties
Environment
Application

This allows advanced routing.

For example:

Application logs → application file
Errors → error file
Audit events → audit destination

⸻

123. Separate Error File Concept

Conceptually:

logs/
    app-2026-08-22.log
    error-2026-08-22.log

Normal logs:

Information
Warning

Error logs:

Error
Critical

This is useful when operations teams need a quick error-only file.

⸻

124. Audit Log Should Be Different

Don’t assume:

Application log = Audit log

Application log:

EmployeeService called

Audit:

User 500 changed employee 101 salary

Audit logs often require:

Longer retention
Restricted access
Tamper-resistant storage
Clear user identity
Business action
Timestamp
Result

⸻

125. Logging and Privacy

Logs can accidentally expose:

Name
Email
Phone
Address
Account information
Tokens
Passwords

Use data minimization.

Instead of:
```cs
_logger.LogInformation("Full user object {@User}", user);
```
prefer:
```cs
_logger.LogInformation("User {UserId} updated profile", user.Id);
```
⸻

126. Logging and GDPR/Compliance

Depending on your system and jurisdiction, logs may contain personal information.

Therefore define:

What is logged?
Who can access it?
How long is it retained?
Where is it stored?
How is it protected?

Logging should be part of your security design.

⸻

127. Log File Permissions

For local files:

Application
     ↓
logs/app.log

Ensure only appropriate identities/users can read/write logs.

Don’t give everyone:

Full Control

unless required.

⸻

128. File Logging in Production

Recommended:

Rolling
+
Retention
+
Restricted permissions
+
Structured format
+
Centralization where appropriate

Example:

logs/
    app-2026-08-20.json
    app-2026-08-21.json
    app-2026-08-22.json



## 129. Local File vs Centralized Logging

#### Local file:
Good for:
- Single server
- Small applications
- Offline diagnostics
- Simple deployments

#### Centralized
Better for:
- Multiple servers
- Containers
- Microservices
- Cloud
- Production monitoring

Architecture:

Server1 ─┐
Server2 ─┤
Server3 ─┼──> Central Log Platform
Server4 ─┘

⸻

130. Containers and Logs

In containers, writing exclusively to local files can be problematic because containers can be replaced.

A common approach is:

Application
    ↓
Console JSON logs
    ↓
Container runtime
    ↓
Log collector
    ↓
Central logging system

Therefore cloud/container deployments often favor stdout/stderr + centralized collection.

⸻

131. Logging Pipeline in a Modern System

A mature system might be:
```
                    .NET Application
                           |
                           v
                        ILogger
                           |
                           v
                    Logging Framework
                           |
               +-----------+-----------+
               |                       |
               v                       v
          Structured Logs          Telemetry
               |                       |
               v                       v
          Log Collector          OpenTelemetry
               |                       |
               +-----------+-----------+
                           |
                           v
                   Central Platform
                           |
             +-------------+-------------+
             |             |             |
             v             v             v
           Search       Dashboard       Alert
```
⸻

132. Alerts

Logging becomes much more useful when alerts are built on top.

Examples:

Critical error detected

or:

More than 100 errors in 5 minutes

or:

Payment failures > 5%

or:

Database connection failures increasing

⸻

133. Logging vs Monitoring

Logging

Individual events

Example:

Order 1001 payment failed.

Monitoring

System health

Example:

Payment failure rate = 5.2%

Both are needed.

⸻

134. Logging vs Tracing

Log

Payment API failed.

Trace

Request
 ↓
Order API 10ms
 ↓
Payment Service 30ms
 ↓
Bank API 900ms
 ↓
Timeout

Tracing explains the journey.

⸻

135. OpenTelemetry + .NET

A modern distributed system can use:

.NET
 ↓
OpenTelemetry
 ↓
Logs
Metrics
Traces
 ↓
Backend

This is more advanced than simple application logging.

⸻

136. Production Logging Levels

A reasonable starting point:

Trace        OFF
Debug        OFF
Information  ON
Warning      ON
Error        ON
Critical     ON

But exact levels should be based on application needs.

For framework categories:

Microsoft → Warning

is often a good starting point.

⸻

137. Production Logging Best Practices

1. Use ILogger<T>
```cs
ILogger<EmployeeService>
```
2. Use structured logging
```cs
"Employee {EmployeeId} created"
```
3. Include useful context

EmployeeId
OrderId
JobId
CorrelationId

4. Don’t log secrets

Never:

Password
JWT
API key
Private key
OTP

5. Use appropriate levels

Don’t make everything Error.

6. Use rolling files

Don’t allow unlimited file growth.

7. Use retention

Delete/archive old logs according to policy.

8. Centralize logs for multiple servers.

9. Use correlation IDs.

10. Use metrics/traces for observability.



138. Complete ILogger Mental Model

Remember:
```
ILogger
    |
    | LogInformation()
    | LogWarning()
    | LogError()
    | LogCritical()
    |
    v
Log Event
    |
    v
Logger infrastructure
    |
    v
Providers
    |
    v
Destinations
```


139. Complete LoggerFactory Mental Model

Remember:
```
ILoggerFactory
      |
      | CreateLogger<T>()
      |
      v
  ILogger<T>
      |
      | LogInformation()
      |
      v
Logging Providers
      |
      +---- Console
      +---- Debug
      +---- EventLog
      +---- File
      +---- Cloud
```
LoggerFactory is a concrete implementation of the ILoggerFactory abstraction.

⸻

140. Complete Serilog Mental Model

Remember:
```
.NET Application
      |
      v
   ILogger
      |
      v
   Serilog
      |
      +---- Minimum Level
      |
      +---- Enrichment
      |
      +---- Filtering
      |
      +---- Formatting
      |
      +---- Sinks
               |
       +-------+-------+
       |       |       |
       v       v       v
     File   Console  Central
```
⸻

141. Built-in Logging vs Serilog

Feature	Built-in .NET	Serilog
ILogger	✅	Uses it
Console	✅	✅
Debug	✅	Via configuration/integration
Basic configuration	✅	✅
File logging	Not built into the core abstraction	✅
Rolling files	Not built into core	✅
Structured logging	✅	Excellent
Enrichment	Limited/basic infrastructure	✅
Many sinks	Provider-based	✅
JSON	✅ with appropriate formatter/provider	✅
Centralized systems	Providers/integrations	Many integrations

The important point is that Serilog does not replace the ILogger abstraction in your application code. You can continue writing:

ILogger<EmployeeService>

while Serilog handles the actual logging pipeline.


142. Recommended Architecture for Your .NET API

For a typical application:
```
                         Browser/Frontend
                                |
                                v
                               IIS
                                |
                                v
                         ASP.NET Core API
                                |
                 +--------------+--------------+
                 |              |              |
                 v              v              v
            Controller       Service       Middleware
                 |              |
                 +--------------+
                                |
                                v
                            Repository
                                |
                                v
                            Database
                                |
                                v
                         ILogger<T>
                                |
                                v
                             Serilog
                                |
                  +-------------+-------------+
                  |             |             |
                  v             v             v
               Console        File        Central Log
                              |
                              v
                       Rolling + Retention
```


143. Recommended Architecture for Background Service
```
Windows Service / Worker
          |
          v
    BackgroundService
          |
          v
      ILogger<Worker>
          |
          v
        Serilog
          |
       +--+--+
       |     |
       v     v
     File  Central
```
⸻

144. Recommended Log Fields

For important production events, useful fields include:

Timestamp
Level
Message
Category
EventId
Application
Environment
Version
MachineName
UserId
RequestId
CorrelationId
JobId
Exception
Duration
Business identifiers

Don’t add everything blindly. Log what is useful and safe.

⸻

145. Example of a High-Quality Log

Conceptually:
```json
{
  "Timestamp": "2026-08-22T01:50:10Z",
  "Level": "Error",
  "Application": "EmployeeAPI",
  "Environment": "Production",
  "Version": "2.5.1",
  "MachineName": "SERVER02",
  "Category": "EmployeeService",
  "EventId": 2001,
  "CorrelationId": "ABC123",
  "EmployeeId": 101,
  "Message": "Failed to create employee",
  "Exception": {
    "Type": "SqlException",
    "Message": "Database connection failed"
  }
}
```
This is much more useful than:

ERROR: Something went wrong

146. Complete Flow When You Write a Log

Suppose code says:
```cs
_logger.LogError(ex, "Failed to create employee {EmployeeId}", employeeId);
```
Think:

1. Application calls ILogger
             ↓
2. Logger has a category
             ↓
3. Logging system checks enabled level
             ↓
4. Event is created
             ↓
5. Exception + properties are attached
             ↓
6. Providers/framework process event
             ↓
7. Formatter creates output
             ↓
8. Destination receives it
             ↓
9. File/Console/Central system stores it
             ↓
10. Monitoring/search/alerting can consume it

⸻

147. The Most Important Difference: ILogger, ILoggerFactory, LoggerFactory

Memorize this table:

Concept	Meaning
ILogger	Writes logs
ILogger<T>	Writes logs with category based on T
ILoggerFactory	Creates ILogger instances
LoggerFactory	Concrete implementation of ILoggerFactory
ILoggerProvider	Provides logging implementation/destination
Serilog	Third-party logging framework
Serilog Sink	Serilog destination
Log Level	Controls severity/detail
Scope	Shared contextual information
Correlation ID	Connects related operations
Enrichment	Adds common properties
Rolling	Creates new log files
Retention	Controls old log storage
Structured Logging	Logs with named properties
Audit Log	Records important user/business actions
Centralized Logging	Collects logs from multiple systems
OpenTelemetry	Observability/telemetry framework

⸻

148. Final Learning Map

If you want to master .NET logging, learn it in this exact order:

LEVEL 1 — BASIC
│
├── What is logging?
├── Why logging?
├── ILogger
├── ILogger<T>
├── LogTrace
├── LogDebug
├── LogInformation
├── LogWarning
├── LogError
└── LogCritical
LEVEL 2 — .NET LOGGING ARCHITECTURE
│
├── ILogger
├── ILoggerFactory
├── LoggerFactory
├── ILoggerProvider
├── Logging categories
├── Providers
└── Dependency Injection
LEVEL 3 — CONFIGURATION
│
├── appsettings.json
├── appsettings.Development.json
├── appsettings.Production.json
├── Minimum level
├── Category filtering
├── Microsoft logs
└── ClearProviders()
LEVEL 4 — GOOD LOGGING
│
├── Structured logging
├── Named properties
├── Exceptions
├── Event IDs
├── Scopes
└── Performance considerations
LEVEL 5 — FILE LOGGING
│
├── File providers
├── Serilog
├── Rolling files
├── Size limits
├── Retention
├── JSON files
└── File permissions
LEVEL 6 — WEB APPLICATION
│
├── Controller logging
├── Service logging
├── Repository logging
├── Middleware logging
├── HTTP request logging
├── Global exception handling
└── Correlation IDs
LEVEL 7 — BACKGROUND SERVICES
│
├── Worker logging
├── Job IDs
├── Retry logging
├── Database operation logging
└── Background exception handling
LEVEL 8 — SECURITY
│
├── Security logs
├── Audit logs
├── Sensitive data
├── Secret protection
├── Log permissions
└── Retention
LEVEL 9 — PRODUCTION
│
├── Rolling
├── Retention
├── JSON
├── Enrichment
├── Multiple destinations
├── Centralized logging
├── Alerts
└── Monitoring
LEVEL 10 — ADVANCED
│
├── LoggerMessage
├── Source-generated logging
├── High-performance logging
├── Elasticsearch
├── Seq
├── Loki
├── Cloud logging
├── Metrics
├── Distributed tracing
└── OpenTelemetry

The single diagram to remember

                         YOUR .NET CODE
                              |
                              v
                         ILogger<T>
                              |
                +-------------+-------------+
                |                           |
                v                           v
         Logging Configuration        ILoggerFactory
                |                           |
                +-------------+-------------+
                              |
                              v
                    Logging Infrastructure
                              |
                    +---------+---------+
                    |         |         |
                    v         v         v
                 Provider  Provider  Provider
                    |         |         |
                    v         v         v
                 Console    File    EventLog
                              |
                              v
                       Serilog / Other
                              |
               +--------------+--------------+
               |              |              |
               v              v              v
             File          Database       Central Log
               |                             |
               v                             v
          Rolling/Retention             Search/Dashboard
                                             |
                                             v
                                           Alerts

Core rule: your application should normally depend on ILogger<T>, not directly on files, Serilog, databases, or logging servers. The logging infrastructure underneath can be changed without rewriting your business code.

And the most important relationship is:

ILoggerFactory → creates ILogger
ILogger        → writes log events
ILoggerProvider → connects logging to a provider/destination
LoggerFactory  → concrete implementation of ILoggerFactory
Serilog        → powerful third-party logging framework
Sink           → Serilog's output destination