# IHttpClientFactory

- `IHttpClientFactory` is an interface in **ASP.NET Core** that is used to **create and manage `HttpClient` objects**.
- It is the **recommended way** to create `HttpClient` instances in ASP.NET Core applications.
- Instead of creating `HttpClient` manually, you ask the factory to create one for you.


### Namespace
```csharp
using System.Net.Http;
```

**Why Do We Need IHttpClientFactory?**
Before `IHttpClientFactory`, developers usually created `HttpClient` like this:
```csharp
HttpClient client = new HttpClient();
```
or:
```csharp
using HttpClient client = new HttpClient();
```

**Creating many `HttpClient` objects can cause problems such as:**
- Too many open connections
- Socket exhaustion
- Difficult configuration
- Difficult testing
- Duplicate code

`IHttpClientFactory` solves these problems by creating and managing `HttpClient` instances efficiently.

### How It Works
```text
Application
      │
      ▼
IHttpClientFactory
      │
      ▼
Creates HttpClient
      │
      ▼
HTTP Request
      │
      ▼
Web Server
```

---

## How To Use:

## Register IHttpClientFactory
- Before using it, register it in **Program.cs**.

```csharp
builder.Services.AddHttpClient();
```
- This adds `IHttpClientFactory` to Dependency Injection (DI).


# Inject IHttpClientFactory
```csharp
public class WeatherService
{
    private readonly IHttpClientFactory _factory;

    public WeatherService(IHttpClientFactory factory)
    {
        _factory = factory;
    }
}
```

---

## Create HttpClient

```csharp
HttpClient client = _factory.CreateClient();
```
- Now you can use `client` normally.


### Complete Example
```csharp
public class WeatherService
{
    private readonly IHttpClientFactory _factory;

    public WeatherService(IHttpClientFactory factory)
    {
        _factory = factory;
    }

    public async Task<string> GetWeather()
    {
        HttpClient client = _factory.CreateClient();

        return await client.GetStringAsync("https://example.com/api/weather");
    }
}
```

---

## Types of IHttpClientFactory

`IHttpClientFactory` supports three types of clients:

1. Basic Client
2. Named Client
3. Typed Client

> **Note:** Generated Clients are an advanced topic often built using third-party libraries (such as Refit) or source generators. They are separate from the built-in factory and can be learned later.

---

## 1. Basic Client
- A basic client has no special configuration.

### Register
```csharp
builder.Services.AddHttpClient();
```

### Create
```csharp
HttpClient client = _factory.CreateClient();
```

- Use this when every request uses the default configuration.

---

## 2. Named Client
- A Named Client has a unique name and its own configuration.
- This is useful when your application communicates with multiple APIs.


## Register
```csharp
builder.Services.AddHttpClient(
    "GitHub",
    client =>
    {
        client.BaseAddress = new Uri("https://api.github.com/");
    });
```


## Create
```csharp
HttpClient client = _factory.CreateClient("GitHub");
```

- Now every time you create the `"GitHub"` client, it already has the configured `BaseAddress`.


**Example:**
```csharp
HttpClient client = _factory.CreateClient("GitHub");

string data = await client.GetStringAsync("users");
```

---

## 3. Typed Client
- A dedicated service class wrapping HttpClient.

**Simple Meaning:**
```text
HttpClient + Business Logic
```

### Example Class:

**Registration:**
```cs
builder.Services.AddHttpClient<EmployeeApiClient>(
    client =>
    {
        client.BaseAddress = new Uri("https://api.company.com/");
    });
```

```cs
public class EmployeeApiClient
{
    private readonly HttpClient _client;

    public EmployeeApiClient(HttpClient client)
    {
        _client = client;
    }

    public async Task<string>GetEmployees()
    {
        return await _client.GetStringAsync("employees");
    }
}
```

**Usage:**
```cs
public class EmployeeService
{
    private readonly EmployeeApiClient _api;

    public EmployeeService(EmployeeApiClient api)
    {
        _api = api;
    }
}
```


---
---

## Comparison

| Feature | Basic Client | Named Client | Typed Client |
|---------|--------------|--------------|--------------|
| Configuration | Default | Named configuration | Class-based configuration |
| Reusable | Yes | Yes | Yes |
| Best For | Simple apps | Multiple APIs | Large applications |
| Easy to Test | No | Moderate | Yes |

---

# Advantages

- Recommended by Microsoft
- Prevents socket exhaustion
- Reuses HTTP connections efficiently
- Works with Dependency Injection
- Centralizes `HttpClient` configuration
- Makes testing easier
- Supports Basic, Named, and Typed clients

---

# Limitations

- Available in ASP.NET Core applications
- Requires Dependency Injection
- Slightly more setup than creating `HttpClient` directly

---

# Best Practices

- Use `IHttpClientFactory` in ASP.NET Core applications.
- Use **Basic Client** for simple scenarios.
- Use **Named Client** when calling multiple APIs with different configurations.
- Use **Typed Client** for large projects where HTTP logic should be encapsulated.
- Register clients once in `Program.cs`.

---

# Interview Questions

### 1. What is IHttpClientFactory?

It is an interface that creates and manages `HttpClient` instances in ASP.NET Core.

---

### 2. Why should we use IHttpClientFactory?

To efficiently manage `HttpClient` instances, reuse connections, avoid socket exhaustion, and centralize configuration.

---

### 3. What are the types of clients supported by IHttpClientFactory?

- Basic Client
- Named Client
- Typed Client

---

### 4. What is a Named Client?

A Named Client is a `HttpClient` with a unique name and predefined configuration.

---

### 5. What is a Typed Client?

A Typed Client is a custom class that receives a configured `HttpClient` through dependency injection.

---