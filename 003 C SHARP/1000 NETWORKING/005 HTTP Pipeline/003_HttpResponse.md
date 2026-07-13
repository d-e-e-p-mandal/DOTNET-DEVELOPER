# HttpResponse

## What is HttpResponse?

`HttpResponse` is a class in **ASP.NET Core** that represents the **HTTP response** sent from the server to the client.

It contains all the information that the server sends back after processing an HTTP request.

The response can include:

- Status Code
- Response Headers
- Cookies
- Response Body
- Content Type

---

# Namespace

```csharp
using Microsoft.AspNetCore.Http;
```

---

# Why Do We Need HttpResponse?

When a client sends a request to the server, the server must send a response.

The response tells the client:

- Was the request successful?
- What data should be displayed?
- What is the response status?
- Should cookies be stored?
- What type of data is being returned?

All this information is managed by the `HttpResponse` class.

---

# How It Works

```text
Client
   │
   │ HTTP Request
   ▼
ASP.NET Core Application
   │
   ▼
HttpResponse
   │
   │ HTTP Response
   ▼
Client
```

---

# Access HttpResponse

`HttpResponse` is accessed through `HttpContext`.

```csharp
HttpResponse response = HttpContext.Response;
```

---

# Response Flow

```text
Client
   │
   ▼
HttpContext
   │
   ▼
HttpResponse
   │
   ▼
Client
```

---

# Common Properties

| Property | Description |
|----------|-------------|
| StatusCode | Gets or sets the HTTP status code |
| Headers | Gets the response headers |
| Cookies | Gets the response cookies |
| ContentType | Gets or sets the response content type |
| ContentLength | Gets or sets the response content length |
| Body | Gets the response body stream |
| HasStarted | Indicates whether the response has started |

---

# Property 1: StatusCode

Gets or sets the HTTP status code.

```csharp
HttpContext.Response.StatusCode = 200;
```

Example

```csharp
HttpContext.Response.StatusCode = 404;
```

---

# Common Status Codes

| Status Code | Meaning |
|-------------|---------|
| 200 | OK |
| 201 | Created |
| 204 | No Content |
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

# Property 2: Headers

Adds or reads response headers.

```csharp
HttpContext.Response.Headers.Add(
    "App-Version",
    "1.0");
```

---

# Property 3: Cookies

Adds cookies to the response.

```csharp
HttpContext.Response.Cookies.Append(
    "Theme",
    "Dark");
```

The browser stores this cookie and sends it back in future requests.

---

# Property 4: ContentType

Specifies the type of data being returned.

```csharp
HttpContext.Response.ContentType =
    "application/json";
```

Common Content Types

| Content Type | Purpose |
|--------------|---------|
| text/plain | Plain Text |
| text/html | HTML |
| application/json | JSON |
| application/xml | XML |
| image/png | PNG Image |

---

# Property 5: ContentLength

Specifies the size of the response body.

```csharp
HttpContext.Response.ContentLength = 256;
```

The value is in **bytes**.

---

# Property 6: Body

Represents the response body stream.

```csharp
Stream body =
    HttpContext.Response.Body;
```

The response body can contain:

- Text
- JSON
- HTML
- XML
- Images
- Files

---

# Property 7: HasStarted

Indicates whether the response has already started.

```csharp
bool started =
    HttpContext.Response.HasStarted;
```

Output

```text
true
```

or

```text
false
```

---

# Write Response

Use `WriteAsync()` to write data into the response body.

```csharp
await HttpContext.Response.WriteAsync(
    "Hello ASP.NET Core");
```

Output

```text
Hello ASP.NET Core
```

---

# Example 1 - Return Plain Text

```csharp
public async Task Index()
{
    HttpContext.Response.ContentType =
        "text/plain";

    await HttpContext.Response.WriteAsync(
        "Hello World");
}
```

---

# Example 2 - Return JSON

```csharp
public async Task Index()
{
    HttpContext.Response.ContentType =
        "application/json";

    await HttpContext.Response.WriteAsync(
        "{ \"name\":\"John\" }");
}
```

Output

```json
{
    "name":"John"
}
```

---

# Example 3 - Set Status Code

```csharp
public IActionResult Index()
{
    HttpContext.Response.StatusCode = 404;

    return Content("Page Not Found");
}
```

---

# Example 4 - Add Cookie

```csharp
public IActionResult Index()
{
    HttpContext.Response.Cookies.Append(
        "Language",
        "English");

    return Content("Cookie Added");
}
```

---

# Example 5 - Add Header

```csharp
public IActionResult Index()
{
    HttpContext.Response.Headers.Add(
        "App-Version",
        "1.0");

    return Content("Header Added");
}
```

---

# HttpResponse Structure

```text
HttpResponse
│
├── StatusCode
├── Headers
├── Cookies
├── ContentType
├── ContentLength
├── Body
└── HasStarted
```

---

# Advantages

- Sends data back to the client.
- Supports custom status codes.
- Supports custom headers.
- Supports cookies.
- Supports different content types.
- Easy to write response data.

---

# Limitations

- Represents only the outgoing response.
- Exists only during the current HTTP request.
- Once the response has started, some properties (such as headers and status code) can no longer be modified.

---

# Best Practices

- Set the correct **Content-Type**.
- Return the appropriate HTTP status code.
- Add headers before writing the response body.
- Avoid modifying headers after the response has started.
- Use asynchronous methods such as `WriteAsync()` for writing response data.

---

# Interview Questions

### 1. What is HttpResponse?

`HttpResponse` represents the HTTP response sent from the server to the client.

---

### 2. How do you access HttpResponse?

```csharp
HttpResponse response =
    HttpContext.Response;
```

---

### 3. Which property sets the HTTP status code?

```csharp
HttpContext.Response.StatusCode
```

---

### 4. Which property sets the response content type?

```csharp
HttpContext.Response.ContentType
```

---

### 5. Which method writes data to the response body?

```csharp
await HttpContext.Response.WriteAsync(
    "Hello");
```

---

### 6. Which property is used to add cookies?

```csharp
HttpContext.Response.Cookies
```

---

### 7. Which property is used to add response headers?

```csharp
HttpContext.Response.Headers
```

---

# HttpResponse vs HttpRequest

| HttpResponse | HttpRequest |
|--------------|-------------|
| Represents the outgoing response | Represents the incoming request |
| Sent by the server | Sent by the client |
| Contains status code, headers, cookies, and response body | Contains method, URL, headers, query, cookies, and request body |
| Accessed using `HttpContext.Response` | Accessed using `HttpContext.Request` |

---
