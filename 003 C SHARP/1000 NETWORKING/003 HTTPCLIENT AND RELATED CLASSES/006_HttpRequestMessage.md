# HttpRequestMessage

- `HttpRequestMessage` is a class in .NET that represents an **HTTP request**.
- It contains all the information needed to send a request to a web server.

This information includes:
- HTTP Method
- Request URL
- Request Headers
- Request Body (Content)
- HTTP Version


### Namespace
```csharp
using System.Net.Http;
```


**Why Do We Need HttpRequestMessage?:**
- Normally, `HttpClient` provides simple methods like:

```csharp
await client.GetAsync(url);

await client.PostAsync(url, content);
```

- These methods are enough for simple requests.
However, when you need more control over the request, you use `HttpRequestMessage`.
**Examples:**
- Add custom headers
- Set HTTP method manually
- Send JSON data
- Change HTTP version
- Configure request properties


### How It Works
```text
Application
      │
      ▼
HttpRequestMessage
      │
      ▼
HttpClient
      │
      ▼
Web Server
```

- `HttpRequestMessage` stores the request information.
- `HttpClient` sends the request.

---

# Create an HttpRequestMessage

```csharp
HttpRequestMessage request = new HttpRequestMessage();
```


## Create Request with Method and URL
```csharp
HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, "https://example.com/api/users");
```

---

## Main Constructor

```csharp
HttpRequestMessage(HttpMethod method, string requestUri)
```

| Parameter | Description |
|-----------|-------------|
| method | HTTP method (GET, POST, PUT, DELETE, etc.) |
| requestUri | URL of the request |

---

# Common Properties

| Property | Description |
|----------|-------------|
| Method | HTTP method |
| RequestUri | Request URL |
| Headers | Request headers |
| Content | Request body |
| Version | HTTP version |

---

### Property 1: Method
Specifies which HTTP method will be used.
**Example:**
```csharp
request.Method = HttpMethod.Get;
```
```csharp
request.Method = HttpMethod.Post;
```


### Property 2: RequestUri
- Specifies the destination URL.
```csharp
request.RequestUri = new Uri("https://example.com/api/users");
```


### Property 3: Headers
- Adds custom request headers.
```csharp
request.Headers.Add("App-Version", "1.0");
```

### Property 4: Content
Used to send data to the server.

```csharp
using System.Text;

request.Content =
    new StringContent(
        "{ \"name\": \"John\" }",
        Encoding.UTF8,
        "application/json");
```

---

### Property 5: Version
Sets the HTTP protocol version.
```csharp
request.Version = new Version(2, 0);
```

**Example:**
```text
HTTP/2
```

---

## Send HttpRequestMessage
After creating the request, send it using `HttpClient`.

```csharp
HttpClient client = new HttpClient();

HttpResponseMessage response = await client.SendAsync(request);
```

---

# Example 1 - GET Request

```csharp
HttpClient client = new HttpClient();

HttpRequestMessage request =
    new HttpRequestMessage(
        HttpMethod.Get,
        "https://example.com/api/users");

HttpResponseMessage response =
    await client.SendAsync(request);
```

---

# Example 2 - POST Request

```csharp
using System.Text;

HttpClient client = new HttpClient();

HttpRequestMessage request =
    new HttpRequestMessage(
        HttpMethod.Post,
        "https://example.com/api/users");

request.Content =
    new StringContent(
        "{ \"name\": \"John\" }",
        Encoding.UTF8,
        "application/json");

HttpResponseMessage response =
    await client.SendAsync(request);
```

---

# Example 3 - Add Custom Header

```csharp
HttpClient client = new HttpClient();

HttpRequestMessage request =
    new HttpRequestMessage(
        HttpMethod.Get,
        "https://example.com/api/users");

request.Headers.Add(
    "App-Version",
    "1.0");

HttpResponseMessage response = await client.SendAsync(request);
```

---

# Example 4 - Authorization Header

```csharp
using System.Net.Http.Headers;

HttpRequestMessage request =
    new HttpRequestMessage(
        HttpMethod.Get,
        "https://example.com/api/users");

request.Headers.Authorization =
    new AuthenticationHeaderValue(
        "Bearer",
        "your_token");
```

---

# Request Structure

```text
HttpRequestMessage
│
├── Method
├── RequestUri
├── Headers
├── Content
└── Version
```

---

# Advantages

- Provides complete control over an HTTP request.
- Supports all HTTP methods.
- Allows custom headers.
- Allows sending request content.
- Allows configuring HTTP version.

---

# Limitations

- Requires more code than `GetAsync()` or `PostAsync()`.
- Usually unnecessary for simple requests.

---

# When Should You Use HttpRequestMessage?

Use `HttpRequestMessage` when you need to:

- Set custom headers
- Configure the HTTP method manually
- Send request content
- Configure the HTTP version
- Create advanced HTTP requests

For simple GET or POST requests, `GetAsync()` and `PostAsync()` are usually sufficient.

---

# Best Practices

- Create a new `HttpRequestMessage` for each request.
- Dispose of the request after use if it is no longer needed.
- Use `SendAsync()` to send the request.
- Add only the headers required by the API.
- Keep the request object focused on a single HTTP request.

---

# Interview Questions

### 1. What is HttpRequestMessage?

`HttpRequestMessage` represents an HTTP request that will be sent to a web server.

---

### 2. What information does HttpRequestMessage contain?

It contains:

- HTTP Method
- Request URL
- Headers
- Content
- HTTP Version

---

### 3. Which method is used to send an HttpRequestMessage?

`SendAsync()` of `HttpClient`.

Example:

```csharp
await client.SendAsync(request);
```

---

### 4. Can HttpRequestMessage send data to the server?

Yes. The request body is assigned to the `Content` property.

---

### 5. When should HttpRequestMessage be used?

When you need more control over the request than what `GetAsync()` or `PostAsync()` provides.

---