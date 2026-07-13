# HttpMessageHandler

- `HttpMessageHandler` is an **abstract base class** in .NET that is responsible for **sending HTTP requests and receiving HTTP responses**.
- It is the **foundation of the HttpClient request pipeline**.
- Every handler used by `HttpClient` is ultimately derived from `HttpMessageHandler`.


### Namespace

```csharp
using System.Net.Http;
```


# Why Do We Need HttpMessageHandler?
- `HttpClient` itself does **not** directly communicate with the server.
- Instead, it passes the request to a `HttpMessageHandler`, which is responsible for sending the request over the network and returning the response.
- Without a `HttpMessageHandler`, `HttpClient` cannot send HTTP requests.



# How It Works

```text
Application
      │
      ▼
HttpClient
      │
      ▼
HttpMessageHandler
      │
      ▼
Web Server
      │
      ▼
HttpMessageHandler
      │
      ▼
HttpClient
      │
      ▼
Application
```

---

# Class Hierarchy

```text
HttpMessageHandler (Abstract)
        ▲
        │
 ┌──────┴──────────────┐
 │                     │
 ▼                     ▼
HttpClientHandler   DelegatingHandler
                           ▲
                           │
                    Custom Handler
```

- `HttpMessageHandler` is the base class.
- `HttpClientHandler` sends requests to the server.
- `DelegatingHandler` intercepts requests and responses.


### HttpMessageHandler Abstract Class?
- Yes.
- `HttpMessageHandler` is an **abstract class**, so you **cannot create its object directly**.
- 
❌ Incorrect: 
```csharp
HttpMessageHandler handler = new HttpMessageHandler();
```

This will cause a compilation error.

-> 
## Use a Derived Class Instead
- Use a class that inherits from `HttpMessageHandler`, such as `HttpClientHandler`.

```csharp
HttpClientHandler handler = new HttpClientHandler();

HttpClient client = new HttpClient(handler);
```

## Main Method

`HttpMessageHandler` contains one important method.

```csharp
protected abstract Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken);
```

This method is responsible for sending an HTTP request and returning an HTTP response.


**Request Flow:**
```text
HttpClient
      │
      ▼
SendAsync()
      │
      ▼
Server
```
- Every HTTP request eventually reaches the `SendAsync()` method.

---

## Creating a Custom HttpMessageHandler

Since `HttpMessageHandler` is abstract, you must inherit from it.

```csharp
using System.Net.Http;

public class MyHandler : HttpMessageHandler
{
     protected override async Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
     {
            return new HttpResponseMessage(System.Net.HttpStatusCode.OK);
     }
}
```

---

# Using Custom HttpMessageHandler

```csharp
MyHandler handler = new MyHandler();

HttpClient client = new HttpClient(handler);
```

Now every request sent by `client` is handled by `MyHandler`.

---

# Difference Between HttpMessageHandler and HttpClientHandler

| HttpMessageHandler | HttpClientHandler |
|--------------------|-------------------|
| Abstract base class | Concrete implementation |
| Cannot be instantiated | Can be instantiated |
| Defines request pipeline | Sends requests to the server |
| Base class for all handlers | Most commonly used handler |

---

# Difference Between HttpMessageHandler and DelegatingHandler

| HttpMessageHandler | DelegatingHandler |
|--------------------|-------------------|
| Base class | Inherits from `HttpMessageHandler` |
| Sends or processes requests | Intercepts requests and responses |
| Abstract class | Concrete base class for custom handlers |
| Lowest level in the pipeline | Used to add custom processing |

---

# Advantages

- Forms the foundation of the HTTP pipeline.
- Provides a common interface for all handlers.
- Allows custom request processing.
- Enables extensibility of `HttpClient`.

---

# Limitations
- Cannot be instantiated directly.
- Requires inheritance to implement `SendAsync()`.
- Most applications do not need to inherit directly from `HttpMessageHandler`; `DelegatingHandler` is usually a better choice for custom processing.

---

### Best Practices
- Do not create an instance of `HttpMessageHandler` directly.
- Use `HttpClientHandler` for normal HTTP communication.
- Use `DelegatingHandler` when you need to inspect or modify requests and responses.
- Inherit directly from `HttpMessageHandler` only when implementing a completely custom transport or handler.

--------------------------
--------------------------

# Interview Questions

### 1. What is HttpMessageHandler?

`HttpMessageHandler` is an abstract base class responsible for sending HTTP requests and receiving HTTP responses.



### 2. Can we create an object of HttpMessageHandler?
- No. It is an abstract class.


### 3. Which method must be implemented when inheriting from HttpMessageHandler?
- `SendAsync()`.

### 4. Which class commonly inherits from HttpMessageHandler?

- `HttpClientHandler`
- `DelegatingHandler`


### 5. When should you inherit directly from HttpMessageHandler?
- Only when you need a completely custom implementation of the HTTP request pipeline. For most scenarios, use `HttpClientHandler` or `DelegatingHandler`.

---