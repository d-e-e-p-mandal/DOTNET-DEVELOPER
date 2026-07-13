# HttpContext

- `HttpContext` is a class in **ASP.NET Core** that represents **one complete HTTP request and its corresponding HTTP response**.
- It contains all the information about the current request being processed by the server.
- Think of `HttpContext` as a **container** that stores everything related to the current HTTP request.
- After the request is completed, the `HttpContext` object is destroyed.


### Namespace

```csharp
using Microsoft.AspNetCore.Http;
```

**Why Do We Need HttpContext?**
- Whenever a client (browser, mobile app, Postman, etc.) sends a request to an ASP.NET Core application, the server creates a new `HttpContext` object.

This object contains:
- Request Information
- Response Information
- User Information
- Session Information
- Connection Information
- Items Shared During Request Processing

Without `HttpContext`, ASP.NET Core would not know:

- Who sent the request
- Which URL was requested
- What headers were sent
- What response should be returned


### How It Works

```text
Client (Browser/Postman)
          │
          │ HTTP Request
          ▼
     ASP.NET Core
          │
          ▼
     HttpContext
     ├── Request
     ├── Response
     ├── User
     ├── Session
     ├── Connection
     └── Items
          │
          ▼
     HTTP Response
          │
          ▼
        Client
```

---

### Life Cycle of HttpContext
- A new `HttpContext` object is created for **every HTTP request**.
- Each request has its **own separate HttpContext**.

```text
Request 1
     │
     ▼
HttpContext #1

Request 2
     │
     ▼
HttpContext #2

Request 3
     │
     ▼
HttpContext #3
```


---

# Common Properties

| Property | Description |
|----------|-------------|
| Request | Gets the current HTTP request |
| Response | Gets the current HTTP response |
| User | Gets the current authenticated user |
| Session | Gets the current session |
| Connection | Gets connection information |
| RequestServices | Accesses Dependency Injection services |
| Items | Stores data during the current request |
| TraceIdentifier | Unique ID of the current request |

---

## Property 1: Request
- Gets information about the incoming request.

```csharp
HttpRequest request = HttpContext.Request;
```

**You can access:**
- URL
- Method
- Headers
- Query String
- Cookies
- Form Data

---

# Property 2: Response
- Gets the outgoing response.

```csharp
HttpResponse response = HttpContext.Response;
```

**You can:**
- Set Status Code
- Set Headers
- Write Response Body
- Set Cookies

---

# Property 3: User

Gets the currently authenticated user.

```csharp
var user = HttpContext.User;
```

Useful for:
- Authentication
- Authorization
- User Identity

---

# Property 4: Session
Gets the current user session.

```csharp
var session = HttpContext.Session;
```

Used to store temporary user data.

Example:

```csharp
HttpContext.Session.SetString(
    "Name",
    "John");
```

---

# Property 5: Connection
- Gets network connection information.

```csharp
var connection = HttpContext.Connection;
```

**Example:**

```csharp
var ip = HttpContext.Connection.RemoteIpAddress;
```

---

# Property 6: RequestServices

Accesses Dependency Injection (DI) services.

```csharp
var service = HttpContext.RequestServices;
```

---

# Property 7: Items

- Stores temporary data during the current request.

```csharp
HttpContext.Items["Message"] = "Hello";
```

Read it later:

```csharp
var value =
    HttpContext.Items["Message"];
```

`Items` exists only during the current request.

---

# Property 8: TraceIdentifier

Gets the unique identifier of the request.

```csharp
Console.WriteLine(HttpContext.TraceIdentifier);
```

Useful for:
- Logging
- Debugging
- Error Tracking

---

# Example 1 - Get Request Method

```csharp
public IActionResult Index()
{
    string method = HttpContext.Request.Method;

    return Content(method);
}
```

Output

```text
GET
```

---

# Example 2 - Get Client IP Address

```csharp
public IActionResult Index()
{
    var ip = HttpContext.Connection.RemoteIpAddress;

    return Content(ip.ToString());
}
```

---

# Example 3 - Write Response

```csharp
public async Task Index()
{
    await HttpContext.Response.WriteAsync("Hello ASP.NET Core");
}
```

Output

```text
Hello ASP.NET Core
```

---

# Example 4 - Store Data in Items

```csharp
HttpContext.Items["UserId"] = 1001;
```

Read later

```csharp
var id =
    HttpContext.Items["UserId"];
```

---

# HttpContext Structure

```text
HttpContext
│
├── Request
├── Response
├── User
├── Session
├── Connection
├── RequestServices
├── Items
└── TraceIdentifier
```

---

# Where Can We Access HttpContext?

You can access `HttpContext` in:

- Controllers
- Middleware
- Razor Pages
- Minimal APIs
- Filters

---

# Advantages

- Stores complete request information.
- Stores complete response information.
- Provides user identity.
- Supports session management.
- Supports dependency injection.
- Provides request-specific storage using `Items`.

---

# Limitations

- Exists only during the current HTTP request.
- Cannot be shared between different requests.
- Should not be stored in static variables or singleton services.

---

# Best Practices

- Use `HttpContext` only for the current request.
- Do not store `HttpContext` for later use.
- Use `Items` for sharing data during the current request.
- Use `RequestServices` only when dependency injection is not directly available.
- Avoid accessing `HttpContext` from background threads after the request has completed.

---

# Interview Questions

### 1. What is HttpContext?

`HttpContext` represents the complete HTTP transaction for a single request and response in ASP.NET Core.

---

### 2. When is HttpContext created?

A new `HttpContext` object is created for every incoming HTTP request.

---

### 3. What does HttpContext contain?

It contains:

- Request
- Response
- User
- Session
- Connection
- RequestServices
- Items
- TraceIdentifier

---

### 4. Can one HttpContext be shared between multiple requests?

No.

Each HTTP request gets its own `HttpContext` object.

---

### 5. Where can HttpContext be accessed?

It can be accessed in:

- Controllers
- Middleware
- Razor Pages
- Minimal APIs
- Filters

---

# HttpContext vs HttpRequest vs HttpResponse

| HttpContext | HttpRequest | HttpResponse |
|-------------|-------------|--------------|
| Represents the complete HTTP transaction | Represents only the incoming request | Represents only the outgoing response |
| Contains Request and Response | Contains request information | Contains response information |
| Created for every request | Accessed through `HttpContext.Request` | Accessed through `HttpContext.Response` |

---
