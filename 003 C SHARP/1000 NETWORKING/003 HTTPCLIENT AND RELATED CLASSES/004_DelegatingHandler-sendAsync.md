# DelegatingHandler : SendAsync() :

- `DelegatingHandler` is a class in .NET that allows you to **intercept, inspect, modify, or process HTTP requests and responses** before they reach the server or before they are returned to the application.

- It works like a **middleware** for `HttpClient`.


### Namespace
```csharp
using System.Net.Http;
```


# Why Do We Need DelegatingHandler?

Sometimes we want to perform an action for **every HTTP request** without writing the same code repeatedly.

**Examples:**
- Add Authentication Token
- Log Requests
- Log Responses
- Measure Request Time
- Validate Requests
- Add Custom Headers

Instead of writing this code in every API call, we can write it once inside a `DelegatingHandler`.


# How It Works

```text
Application
      │
      ▼
HttpClient
      │
      ▼
DelegatingHandler
      │
      ▼
    Server
      │
      ▼
DelegatingHandler
      │
      ▼
Application
```

- The request passes through the handler before reaching the server.
- The response also passes through the handler before reaching the application.

---

# Inheritance

```text
HttpMessageHandler
        ▲
        │
DelegatingHandler
        ▲
        │
Your Custom Handler
```

`DelegatingHandler` inherits from `HttpMessageHandler`.

You create your own handler by inheriting from `DelegatingHandler`.

---

# Create a Custom DelegatingHandler

```csharp
using System.Net.Http;
public class MyHandler : DelegatingHandler
{

}
```

---

# Override SendAsync()
The main method of `DelegatingHandler` is `SendAsync()`.

```csharp
protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
{
    return await base.SendAsync(request, cancellationToken);
}
```

- Every request passes through this method.

---

# Request Flow

```text
Request
   │
   ▼
SendAsync()
   │
   ▼
base.SendAsync()
   │
   ▼
Server
```

---

# Response Flow

```text
Server
   │
   ▼
base.SendAsync()
   │
   ▼
SendAsync()
   │
   ▼
Application
```

---

# Example 1 - Logging Request

```csharp
public class LoggingHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        Console.WriteLine($"Request : {request.Method}");
        Console.WriteLine($"URL : {request.RequestUri}");

        return await base.SendAsync(request, cancellationToken);
    }
}
```


# Example 2 - Logging Response

```csharp
public class LoggingHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        HttpResponseMessage response = await base.SendAsync(request, cancellationToken);

        Console.WriteLine($"Status : {response.StatusCode}");

        return response;
    }
}
```

---

# Example 3 - Add Custom Header

```csharp
public class HeaderHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    {
        request.Headers.Add("App-Version", "1.0");

        return await base.SendAsync(request, cancellationToken);
    }
}
```

Every request automatically includes the custom header.

---

# Example 4 - Add Bearer Token

```csharp
public class AuthHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage> SendAsync(
        HttpRequestMessage request,
        CancellationToken cancellationToken)
    {
        request.Headers.Authorization =
            new System.Net.Http.Headers.AuthenticationHeaderValue(
                "Bearer",
                "your_token");

        return await base.SendAsync(request, cancellationToken);
    }
}
```

---

# Register DelegatingHandler

Register your custom handler in **Program.cs**.

```csharp
builder.Services.AddTransient<LoggingHandler>();
```

---

# Use with IHttpClientFactory : 

[AddHttpMessageHandler](#AddHttpMessageHandler)

```csharp
builder.Services
    .AddHttpClient("MyApi")
    .AddHttpMessageHandler<LoggingHandler>();
```

Now every request made using the `"MyApi"` client passes through `LoggingHandler`.

---

# Multiple DelegatingHandlers

You can use more than one handler.

```text
HttpClient
     │
     ▼
AuthenticationHandler
     │
     ▼
LoggingHandler
     │
     ▼
TimingHandler
     │
     ▼
Server
```

The request passes through each handler in order.

The response returns through the handlers in reverse order.

---

# Advantages

- Reusable code
- Centralized request processing
- Centralized response processing
- Easy logging
- Easy authentication
- Easy header management
- Works with `IHttpClientFactory`

---

# Limitations

- Adds an extra processing step
- Too many handlers can make debugging harder
- Handler order is important

---

# Best Practices

- Keep each handler focused on one responsibility.
- Do not put business logic inside handlers.
- Use handlers for cross-cutting concerns like logging, authentication, and headers.
- Register handlers using Dependency Injection.
- Use with `IHttpClientFactory` for best results.

---

# Interview Questions

### 1. What is DelegatingHandler?

`DelegatingHandler` is a class that intercepts HTTP requests and responses sent by `HttpClient`.

---

### 2. Why do we use DelegatingHandler?

To execute common logic such as logging, authentication, adding headers, or measuring request time for every HTTP request.

---

### 3. Which method must be overridden?

`SendAsync()`.

---

### 4. Can multiple DelegatingHandlers be used?

Yes. Multiple handlers can be chained together.

---

### 5. Does DelegatingHandler process both requests and responses?

Yes. It processes the request before it reaches the server and the response before it reaches the application.

---

------
------
# AddHttpMessageHandler

AddHttpMessageHandler<THandler>() adds a custom message handler into the HttpClient request pipeline. Every request made by that HttpClient passes through the handler before it is sent.

Project Structure

MyProject/
│
├── Program.cs
├── Controllers/
│   └── WeatherController.cs
│
├── Handlers/
│   └── LoggingHandler.cs
│
└── Services/
    └── WeatherService.cs

⸻

Step 1: Create LoggingHandler

Path: Handlers/LoggingHandler.cs

using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;
public class LoggingHandler : DelegatingHandler
{
    protected override async Task<HttpResponseMessage> SendAsync(
        HttpRequestMessage request,
        CancellationToken cancellationToken)
    {
        Console.WriteLine($"Request: {request.Method} {request.RequestUri}");
        HttpResponseMessage response =
            await base.SendAsync(request, cancellationToken);
        Console.WriteLine($"Response: {(int)response.StatusCode}");
        return response;
    }
}

⸻

Step 2: Register the Handler

Path: Program.cs

using Microsoft.Extensions.DependencyInjection;
var builder = WebApplication.CreateBuilder(args);
builder.Services.AddTransient<LoggingHandler>();
builder.Services
    .AddHttpClient("MyApi", client =>
    {
        client.BaseAddress = new Uri("https://jsonplaceholder.typicode.com/");
    })
    .AddHttpMessageHandler<LoggingHandler>();
builder.Services.AddControllers();
var app = builder.Build();
app.MapControllers();
app.Run();

⸻

Step 3: Use the Named HttpClient

Path: Controllers/WeatherController.cs

using Microsoft.AspNetCore.Mvc;
[ApiController]
[Route("[controller]")]
public class WeatherController : ControllerBase
{
    private readonly IHttpClientFactory _factory;
    public WeatherController(IHttpClientFactory factory)
    {
        _factory = factory;
    }
    [HttpGet]
    public async Task<string> Get()
    {
        HttpClient client = _factory.CreateClient("MyApi");
        return await client.GetStringAsync("posts/1");
    }
}

⸻

Request Flow

Browser
    │
    ▼
WeatherController
    │
    ▼
IHttpClientFactory
    │
    ▼
HttpClient ("MyApi")
    │
    ▼
LoggingHandler
    │
    ▼
HttpClientHandler
    │
    ▼
https://jsonplaceholder.typicode.com/posts/1

⸻

Console Output

When you call:

GET /Weather

You will see:

Request: GET https://jsonplaceholder.typicode.com/posts/1
Response: 200

Why use AddHttpMessageHandler?

* Log every request and response.
* Add authentication headers automatically.
* Measure request duration.
* Implement retry or custom processing.
* Keep cross-cutting concerns separate from your business logic.

This pattern is commonly used with IHttpClientFactory in ASP.NET Core applications to build a reusable HTTP request pipeline.