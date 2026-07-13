# RequestDelegate

## What is RequestDelegate?

`RequestDelegate` is a **delegate** in **ASP.NET Core** that represents a method responsible for processing an HTTP request.

It points to the **next middleware** in the ASP.NET Core Middleware Pipeline.

Simply put,

> **`RequestDelegate` is used to pass the current HTTP request to the next middleware.**

---

# Namespace

```csharp
using Microsoft.AspNetCore.Http;
```

---

# Why Do We Need RequestDelegate?

ASP.NET Core applications contain multiple middleware components.

When one middleware finishes its work, it must pass the request to the next middleware.

`RequestDelegate` performs this task.

Without `RequestDelegate`, the request cannot continue through the middleware pipeline.

---

# How It Works

```text
Client
   │
   ▼
Middleware 1
   │
   ▼
RequestDelegate
   │
   ▼
Middleware 2
   │
   ▼
RequestDelegate
   │
   ▼
Middleware 3
   │
   ▼
Controller / Endpoint
```

---

# Delegate Definition

Internally, `RequestDelegate` is defined like this:

```csharp
public delegate Task RequestDelegate(
    HttpContext context);
```

It accepts one parameter:

- `HttpContext`

It returns:

- `Task`

---

# Request Flow

```text
Request
   │
   ▼
Middleware
   │
   ▼
RequestDelegate
   │
   ▼
Next Middleware
```

---

# Where is RequestDelegate Used?

`RequestDelegate` is commonly used in:

- Custom Middleware
- IMiddleware
- Middleware Pipeline

---

# Example 1 - RequestDelegate in Middleware Constructor

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

Here,

`_next` stores the next middleware.

---

# Example 2 - Calling the Next Middleware

```csharp
public async Task InvokeAsync(
    HttpContext context)
{
    await _next(context);
}
```

Explanation:

```text
Current Middleware
        │
        ▼
_next(context)
        │
        ▼
Next Middleware
```

---

# Example 3 - Before and After Request

```csharp
public async Task InvokeAsync(
    HttpContext context)
{
    Console.WriteLine("Before Request");

    await _next(context);

    Console.WriteLine("After Response");
}
```

Execution Order

```text
Request

Before Request
      │
      ▼
Next Middleware
      │
      ▼
Controller
      │
      ▲
Next Middleware
      ▲
After Response
```

---

# Example 4 - Stop the Pipeline

If `_next(context)` is **not** called:

```csharp
public async Task InvokeAsync(
    HttpContext context)
{
    await context.Response.WriteAsync(
        "Pipeline Stopped");
}
```

Result

```text
Request
    │
    ▼
Current Middleware
    │
    ▼
Response Returned

(No Next Middleware)
```

The remaining middleware and endpoint are skipped.

---

# Data Flow

```text
Client
   │
   ▼
Middleware A
   │
   ▼
RequestDelegate
   │
   ▼
Middleware B
   │
   ▼
RequestDelegate
   │
   ▼
Controller
```

---

# Advantages

- Connects middleware components.
- Enables the middleware pipeline.
- Supports asynchronous request processing.
- Allows middleware to execute code before and after the next middleware.
- Makes request processing modular.

---

# Limitations

- Calling `_next(context)` is required to continue the pipeline.
- Forgetting to call `_next(context)` stops the request.
- Incorrect middleware order may affect application behavior.

---

# Best Practices

- Always call `await _next(context)` unless you intentionally want to stop the pipeline.
- Perform request-related work before calling `_next(context)`.
- Perform response-related work after `_next(context)` returns.
- Keep middleware focused on a single responsibility.
- Do not place business logic inside middleware.

---

# Interview Questions

### 1. What is RequestDelegate?

`RequestDelegate` is a delegate that represents a method responsible for processing an HTTP request and passing it to the next middleware.

---

### 2. What parameter does RequestDelegate accept?

```csharp
HttpContext
```

---

### 3. What does RequestDelegate return?

```csharp
Task
```

---

### 4. Why is RequestDelegate used?

It passes the current HTTP request to the next middleware in the pipeline.

---

### 5. What happens if `_next(context)` is not called?

The middleware pipeline stops, and the remaining middleware and endpoint are not executed.

---

### 6. Where is RequestDelegate commonly used?

- Custom Middleware
- IMiddleware
- Middleware Pipeline

---

# RequestDelegate vs IMiddleware

| RequestDelegate | IMiddleware |
|-----------------|-------------|
| Delegate | Interface |
| Represents the next middleware | Used to create custom middleware |
| Passes the request through the pipeline | Implements middleware logic |
| Used inside middleware | Middleware class implements it |

---

# RequestDelegate vs HttpContext

| RequestDelegate | HttpContext |
|-----------------|-------------|
| Passes the request to the next middleware | Contains information about the current HTTP request and response |
| Delegate | Class |
| Used for pipeline execution | Used to access request and response data |

---