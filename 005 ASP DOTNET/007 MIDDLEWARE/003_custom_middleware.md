# Custom Middleware in ASP.NET Core

---

# What is Custom Middleware?

Custom Middleware is user-created middleware.

Used to:
- Process requests
- Process responses
- Add custom logic

---

# Simple Meaning

```text
Custom Middleware = Our Own Request Handler
```

---

# Why Custom Middleware Used?

Used for:
- Logging
- Exception handling
- Authentication
- Request tracking
- Custom security
- Response modification

---

# Middleware Flow

```text
Client Request
        ↓
Custom Middleware
        ↓
Controller
        ↓
Response
        ↓
Custom Middleware
        ↓
Client
```

---

# Middleware Pipeline

```text
Request
  ↓
Middleware 1
  ↓
Middleware 2
  ↓
Custom Middleware
  ↓
Controller
  ↓
Response
```

---

# Creating Custom Middleware

There are 3 main parts:
- Middleware Class
- Invoke Method
- Middleware Registration

---

# 1. Creating Custom Middleware

---

# Create Middleware Folder

```text
Project
│
├── Middleware/
│      └── LoggingMiddleware.cs
```

---

# Example Middleware

```cs
using Microsoft.AspNetCore.Http;

public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext context)
    {
        Console.WriteLine("Request Started");
        // own logic here : before
        await _next(context);
        // own logic after
        Console.WriteLine("Request Finished");
    }
}
```

---

# Explanation

---

# RequestDelegate

```cs
private readonly RequestDelegate _next;
```

## Purpose

Represents next middleware in pipeline.

---

# Constructor

```cs
public LoggingMiddleware(RequestDelegate next)
```

ASP.NET Core automatically injects next middleware.

---

# Invoke()

```cs
public async Task Invoke(HttpContext context)
```

Main middleware method.

Runs on every request.

---

# HttpContext

```cs
HttpContext context
```

Contains:
- Request
- Response
- User
- Headers
- Session

---

# _next(context)

```cs
await _next(context);
```
- Passes request to next middleware.

---

# IMPORTANT

Without:

```cs
await _next(context);
```
- request stops.
- Controller never executes.

---

# Flow

```text
Request Comes
      ↓
Middleware Executes
      ↓
_next(context)
      ↓
Next Middleware Runs
      ↓
Controller Executes
      ↓
Response Returns
```

---

# Middleware Registration

Middleware must be registered in:

```text
Program.cs
```

---

# Example

```cs
app.UseMiddleware<LoggingMiddleware>();
```

---

# Complete Example

```cs
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.UseMiddleware<LoggingMiddleware>();

app.MapControllers();

app.Run();
```

---

# Middleware Execution Order

```text
Request
   ↓
Middleware 1
   ↓
Middleware 2
   ↓
Controller
   ↓
Middleware 2
   ↓
Middleware 1
   ↓
Response
```

---

# Request & Response Handling

Middleware works:
- Before controller
- After controller

---

# Example

```cs
public async Task Invoke(HttpContext context)
{
    Console.WriteLine("Before Request");

    await _next(context);

    Console.WriteLine("After Response");
}
```

---

# Output

```text
Before Request
After Response
```

---

# Exception Middleware

---

# What is Exception Middleware?

Handles application errors globally.

---

# Purpose

Used for:
- Global error handling
- Clean error responses
- Prevent application crash

---

# Exception Middleware Example

```cs
using System.Net;

public class ExceptionMiddleware
{
    private readonly RequestDelegate _next;

    public ExceptionMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch (Exception ex)
        {
            context.Response.StatusCode = 500;

            await context.Response.WriteAsync(
                "Internal Server Error");
        }
    }
}
```

---

# Flow

```text
Request
   ↓
Controller Error
   ↓
Catch Exception
   ↓
Return Error Response
```

---

# Benefits

- Centralized error handling
- Cleaner code
- Common error format

---

# Middleware Registration

```cs
app.UseMiddleware<ExceptionMiddleware>();
```

---

# Production Usage

Mostly added at top of pipeline.

---

# Example

```cs
app.UseMiddleware<ExceptionMiddleware>();

app.UseAuthentication();

app.UseAuthorization();
```

---

# Logging Middleware

---

# What is Logging Middleware?

Middleware used to log:
- Requests
- Responses
- Errors
- Execution time

---

# Purpose

Used for:
- Monitoring
- Debugging
- Tracking requests

---

# Logging Middleware Example

```cs
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(HttpContext context)
    {
        Console.WriteLine(
            $"Request: {context.Request.Path}");

        await _next(context);

        Console.WriteLine(
            $"Response Status: {context.Response.StatusCode}");
    }
}
```

---

# Output Example

```text
Request: /api/employee
Response Status: 200
```

---

# Logging Information

Can log:
- URL
- Method
- Headers
- Response status
- Time taken

---

# Example

```cs
Console.WriteLine(context.Request.Method);
```

---

# Logging Request Method

```text
GET
POST
PUT
DELETE
```

---

# Logging Request Path

```cs
context.Request.Path
```

---

# Logging Response Status

```cs
context.Response.StatusCode
```

---

# Real Logging Systems

Industry uses:
- Serilog
- NLog
- ILogger

---

# Middleware Folder Structure

```text
Project
│
├── Middleware/
│      ├── LoggingMiddleware.cs
│      ├── ExceptionMiddleware.cs
│      ├── AuthenticationMiddleware.cs
```

---

# Middleware Extension Method

Instead of:

```cs
app.UseMiddleware<LoggingMiddleware>();
```

we can create extension methods.

---

# Example

```cs
public static class MiddlewareExtensions
{
    public static IApplicationBuilder
        UseLoggingMiddleware(
            this IApplicationBuilder app)
    {
        return app.UseMiddleware<LoggingMiddleware>();
    }
}
```

---

# Usage

```cs
app.UseLoggingMiddleware();
```

---

# Middleware Order Important

Correct order matters.

---

# Example

```cs
app.UseMiddleware<ExceptionMiddleware>();

app.UseAuthentication();

app.UseAuthorization();
```

---

# Why?

Because:
- Exception middleware should catch all errors

---

# Complete Middleware Pipeline Example

```cs
app.UseHttpsRedirection();

app.UseStaticFiles();

app.UseRouting();

app.UseMiddleware<ExceptionMiddleware>();

app.UseAuthentication();

app.UseAuthorization();

app.UseMiddleware<LoggingMiddleware>();

app.MapControllers();
```

---

# Complete Request Flow

```text
Client Request
        ↓
HTTPS Middleware
        ↓
Routing Middleware
        ↓
Exception Middleware
        ↓
Authentication Middleware
        ↓
Authorization Middleware
        ↓
Logging Middleware
        ↓
Controller
        ↓
Response
```

---

# Advantages of Custom Middleware

- Reusable logic
- Centralized processing
- Cleaner controllers
- Better maintainability

---

# Common Custom Middleware Examples

| Middleware | Purpose |
|---|---|
| Logging Middleware | Request logging |
| Exception Middleware | Error handling |
| JWT Middleware | Token validation |
| Request Timing Middleware | Performance tracking |
| Security Middleware | Security checks |

---

# Real-Life Analogy

| ASP.NET Core Middleware | Real Life |
|---|---|
| Middleware | Security Guard |
| Logging Middleware | CCTV Recorder |
| Exception Middleware | Emergency Handler |
| Request Pipeline | Airport Security Line |
| RequestDelegate | Next Security Gate |