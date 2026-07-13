# Middleware Pipeline

## What is Middleware?

**Middleware** is a software component in **ASP.NET Core** that processes an HTTP request and an HTTP response.

Every incoming request passes through a series of middleware components before reaching the application.

Similarly, every outgoing response passes through the same middleware components in reverse order.

This series of middleware components is called the **Middleware Pipeline**.

---

# What is Middleware Pipeline?

The **Middleware Pipeline** is the sequence of middleware components that process every HTTP request and HTTP response.

Each middleware can:

- Process the request
- Modify the request
- Pass the request to the next middleware
- Stop the request
- Process the response
- Modify the response

---

# Namespace

```csharp
using Microsoft.AspNetCore.Builder;
```

---

# Why Do We Need Middleware Pipeline?

Without middleware, ASP.NET Core cannot process requests.

Middleware performs many important tasks such as:

- Exception Handling
- Routing
- Authentication
- Authorization
- CORS
- Serving Static Files
- Logging
- HTTPS Redirection

---

# How It Works

```text
Client
   │
   │ HTTP Request
   ▼
Middleware 1
   │
   ▼
Middleware 2
   │
   ▼
Middleware 3
   │
   ▼
Controller / Endpoint
   │
   │ HTTP Response
   ▲
Middleware 3
   ▲
Middleware 2
   ▲
Middleware 1
   ▲
Client
```

The request travels **forward** through the pipeline.

The response travels **backward** through the pipeline.

---

# Middleware Flow

```text
Request
   │
   ▼
Middleware A
   │
   ▼
Middleware B
   │
   ▼
Middleware C
   │
   ▼
Endpoint
   ▲
   │
Middleware C
   ▲
Middleware B
   ▲
Middleware A
   ▲
Response
```

---

# Where is Middleware Configured?

Middleware is configured in **Program.cs**.

Example:

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.UseHttpsRedirection();

app.UseRouting();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

Each `Use...()` method adds a middleware to the pipeline.

---

# Middleware Execution Order

Middleware executes in the order in which it is added.

Example:

```text
app.UseA();

app.UseB();

app.UseC();
```

Execution Order

```text
Request

UseA
   │
   ▼
UseB
   │
   ▼
UseC
   │
   ▼
Endpoint
```

Response Order

```text
Endpoint
   ▲
UseC
   ▲
UseB
   ▲
UseA
```

---

# Types of Middleware

ASP.NET Core provides many built-in middleware components.

Examples:

- Exception Handling Middleware
- Static File Middleware
- Routing Middleware
- Authentication Middleware
- Authorization Middleware
- CORS Middleware
- HTTPS Redirection Middleware

You can also create your own custom middleware.

---

# Create Custom Middleware

```csharp
public class LoggingMiddleware
{
}
```

---

# Middleware Constructor

Every middleware receives the next middleware in the pipeline.

```csharp
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(
        RequestDelegate next)
    {
        _next = next;
    }
}
```

---

# InvokeAsync Method

Every middleware contains an `InvokeAsync()` method.

```csharp
public async Task InvokeAsync(
    HttpContext context)
{
    await _next(context);
}
```

`_next(context)` passes the request to the next middleware.

---

# Complete Middleware Example

```csharp
public class LoggingMiddleware
{
    private readonly RequestDelegate _next;

    public LoggingMiddleware(
        RequestDelegate next)
    {
        _next = next;
    }

    public async Task InvokeAsync(
        HttpContext context)
    {
        Console.WriteLine("Before Request");

        await _next(context);

        Console.WriteLine("After Response");
    }
}
```

---

# Register Custom Middleware

Register it in **Program.cs**.

```csharp
app.UseMiddleware<LoggingMiddleware>();
```

---

# Pipeline with Custom Middleware

```text
Client
   │
   ▼
LoggingMiddleware
   │
   ▼
Routing Middleware
   │
   ▼
Authentication Middleware
   │
   ▼
Controller
```

---

# Request and Response Flow

```text
Request
   │
   ▼
LoggingMiddleware
   │
   ▼
Controller
   │
   ▲
LoggingMiddleware
   ▲
Response
```

Notice that the same middleware processes both the request and the response.

---

# Short-Circuiting the Pipeline

A middleware can stop the pipeline and return a response immediately.

Example:

```csharp
public async Task InvokeAsync(
    HttpContext context)
{
    await context.Response.WriteAsync(
        "Request Stopped");
}
```

Since `_next(context)` is **not** called, the remaining middleware and endpoint are never executed.

---

# Advantages

- Modular architecture
- Easy to add or remove features
- Reusable components
- Centralized request processing
- Centralized response processing
- Supports custom middleware

---

# Limitations

- Incorrect middleware order can cause application issues.
- Too many middleware components can slightly increase request processing time.
- A middleware that does not call `_next(context)` stops the pipeline.

---

# Best Practices

- Register middleware in the correct order.
- Keep each middleware focused on a single responsibility.
- Always call `_next(context)` unless intentionally stopping the pipeline.
- Place exception handling middleware near the beginning of the pipeline.
- Place authentication before authorization.
- Use custom middleware only when necessary.

---

# Interview Questions

### 1. What is Middleware?

Middleware is a software component that processes HTTP requests and responses in ASP.NET Core.

---

### 2. What is the Middleware Pipeline?

The Middleware Pipeline is the sequence of middleware components through which every HTTP request and response passes.

---

### 3. Where is the Middleware Pipeline configured?

In **Program.cs**.

---

### 4. Which method passes the request to the next middleware?

```csharp
await _next(context);
```

---

### 5. What happens if `_next(context)` is not called?

The request pipeline stops, and the remaining middleware and endpoint are not executed.

---

### 6. Can a middleware modify both the request and the response?

Yes.

A middleware can inspect or modify the request before calling `_next(context)` and inspect or modify the response after `_next(context)` returns.

---

# Middleware Pipeline vs Middleware

| Middleware | Middleware Pipeline |
|------------|---------------------|
| A single component that processes requests and responses | A sequence of multiple middleware components |
| Performs one specific task | Represents the complete request-processing flow |
| Can pass the request to the next middleware | Contains all middleware in execution order |

---