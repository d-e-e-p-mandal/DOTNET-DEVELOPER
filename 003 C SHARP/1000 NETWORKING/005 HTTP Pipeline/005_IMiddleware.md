# IMiddleware

## What is IMiddleware?

`IMiddleware` is an **interface** in **ASP.NET Core** that is used to create **custom middleware**.

Instead of creating middleware using `RequestDelegate`, you can implement the `IMiddleware` interface.

`IMiddleware` is managed by **Dependency Injection (DI)**, making it easier to inject services into middleware.

---

# Namespace

```csharp
using Microsoft.AspNetCore.Http;
```

---

# Why Do We Need IMiddleware?

ASP.NET Core provides two ways to create custom middleware:

1. Conventional Middleware
2. IMiddleware

`IMiddleware` is useful because:

- It works with Dependency Injection.
- It is easier to test.
- It separates middleware creation from registration.
- It improves code maintainability.

---

# How It Works

```text
Client
   │
   ▼
Middleware Pipeline
   │
   ▼
IMiddleware
   │
   ▼
Controller / Endpoint
   │
   ▲
Response
```

---

# Relationship

```text
IMiddleware (Interface)
        ▲
        │
Custom Middleware
```

Your custom middleware implements the `IMiddleware` interface.

---

# IMiddleware Interface

`IMiddleware` contains one method.

```csharp
Task InvokeAsync(
    HttpContext context,
    RequestDelegate next
);
```

| Parameter | Description |
|-----------|-------------|
| context | Current HTTP request and response |
| next | Executes the next middleware |

---

# Create IMiddleware

```csharp
using Microsoft.AspNetCore.Http;

public class LoggingMiddleware : IMiddleware
{
    public async Task InvokeAsync(
        HttpContext context,
        RequestDelegate next)
    {

    }
}
```

---

# Implement InvokeAsync()

```csharp
public class LoggingMiddleware : IMiddleware
{
    public async Task InvokeAsync(
        HttpContext context,
        RequestDelegate next)
    {
        Console.WriteLine("Before Request");

        await next(context);

        Console.WriteLine("After Response");
    }
}
```

---

# How InvokeAsync() Works

```text
Request
   │
   ▼
InvokeAsync()
   │
   ▼
next(context)
   │
   ▼
Next Middleware
   │
   ▲
Response
   ▲
InvokeAsync()
```

- Code **before** `next(context)` executes before the next middleware.
- Code **after** `next(context)` executes after the response returns.

---

# Register IMiddleware

Register the middleware in **Program.cs**.

```csharp
builder.Services.AddTransient<LoggingMiddleware>();
```

`AddTransient()` creates a new middleware instance for each request.

---

# Add IMiddleware to Pipeline

```csharp
app.UseMiddleware<LoggingMiddleware>();
```

Now the middleware becomes part of the HTTP pipeline.

---

# Complete Example

## Step 1: Create Middleware

```csharp
using Microsoft.AspNetCore.Http;

public class LoggingMiddleware : IMiddleware
{
    public async Task InvokeAsync(
        HttpContext context,
        RequestDelegate next)
    {
        Console.WriteLine("Request Started");

        await next(context);

        Console.WriteLine("Request Completed");
    }
}
```

---

## Step 2: Register Service

```csharp
builder.Services.AddTransient<LoggingMiddleware>();
```

---

## Step 3: Add Middleware

```csharp
app.UseMiddleware<LoggingMiddleware>();
```

---

# Middleware Flow

```text
Client
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
Client
```

---

# Dependency Injection Example

One advantage of `IMiddleware` is that services can be injected through the constructor.

```csharp
public class LoggingMiddleware : IMiddleware
{
    private readonly ILogger<LoggingMiddleware> _logger;

    public LoggingMiddleware(
        ILogger<LoggingMiddleware> logger)
    {
        _logger = logger;
    }

    public async Task InvokeAsync(
        HttpContext context,
        RequestDelegate next)
    {
        _logger.LogInformation("Request Started");

        await next(context);

        _logger.LogInformation("Request Completed");
    }
}
```

---

# Advantages

- Supports Dependency Injection.
- Easy to test.
- Cleaner and more maintainable code.
- Better separation of responsibilities.
- Reusable middleware.

---

# Limitations

- Requires service registration in Dependency Injection.
- Slightly more setup than conventional middleware.
- Should be used only when Dependency Injection is beneficial.

---

# Best Practices

- Register middleware using Dependency Injection.
- Keep middleware focused on a single responsibility.
- Always call `await next(context)` unless intentionally stopping the pipeline.
- Use constructor injection for required services.
- Avoid putting business logic inside middleware.

---

# Interview Questions

### 1. What is IMiddleware?

`IMiddleware` is an interface used to create custom middleware in ASP.NET Core.

---

### 2. Which method must be implemented?

```csharp
InvokeAsync()
```

---

### 3. Why is IMiddleware preferred in some applications?

Because it integrates with Dependency Injection, making middleware easier to test and maintain.

---

### 4. How do you register IMiddleware?

```csharp
builder.Services.AddTransient<LoggingMiddleware>();
```

---

### 5. How do you add IMiddleware to the pipeline?

```csharp
app.UseMiddleware<LoggingMiddleware>();
```

---

### 6. What happens if `next(context)` is not called?

The request pipeline stops, and the remaining middleware and endpoint are not executed.

---

# IMiddleware vs Conventional Middleware

| IMiddleware | Conventional Middleware |
|-------------|-------------------------|
| Interface | Regular class |
| Uses Dependency Injection | Uses constructor with `RequestDelegate` |
| Must be registered in DI | No DI registration required |
| Implements `InvokeAsync()` | Defines `Invoke()` or `InvokeAsync()` |
| Better for service injection | Simpler for basic middleware |

---
