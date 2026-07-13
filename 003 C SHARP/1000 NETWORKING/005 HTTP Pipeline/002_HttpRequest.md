# HttpRequest

## What is HttpRequest?

`HttpRequest` is a class in **ASP.NET Core** that represents the **incoming HTTP request** sent by the client to the server.

It contains all the information sent by the client, such as:

- HTTP Method
- URL
- Headers
- Query String
- Route Values
- Form Data
- Cookies
- Request Body

---

# Namespace

```csharp
using Microsoft.AspNetCore.Http;
```

---

# Why Do We Need HttpRequest?

Whenever a browser, mobile app, or API client sends a request to an ASP.NET Core application, the request contains information such as:

- Which page is requested?
- Which HTTP method is used?
- What headers are included?
- Is there any form data?
- Is there any JSON data?
- Are there any cookies?

All of this information is available through the `HttpRequest` object.

---

# How It Works

```text
Client
   │
   │ HTTP Request
   ▼
HttpRequest
   │
   ▼
ASP.NET Core Application
```

The client sends a request.

`HttpRequest` stores all the request information.

---

# Access HttpRequest

`HttpRequest` is accessed through `HttpContext`.

```csharp
HttpRequest request = HttpContext.Request;
```

---

# Request Flow

```text
Client
   │
   ▼
HttpContext
   │
   ▼
HttpRequest
```

---

# Common Properties

| Property | Description |
|----------|-------------|
| Method | HTTP request method |
| Scheme | HTTP or HTTPS |
| Host | Server host name |
| Path | Requested URL path |
| QueryString | Complete query string |
| Query | Individual query parameters |
| Headers | Request headers |
| Cookies | Request cookies |
| Form | Submitted form data |
| Body | Request body |
| RouteValues | Route parameter values |
| ContentType | Request content type |
| ContentLength | Size of request body |

---

# Property 1: Method

Gets the HTTP request method.

```csharp
string method = HttpContext.Request.Method;

Console.WriteLine(method);
```

Output

```text
GET
```

Possible values:

- GET
- POST
- PUT
- PATCH
- DELETE

---

# Property 2: Scheme

Gets the protocol used.

```csharp
string scheme =
    HttpContext.Request.Scheme;
```

Output

```text
https
```

Possible values:

- http
- https

---

# Property 3: Host

Gets the server host.

```csharp
string host =
    HttpContext.Request.Host.Value;
```

Output

```text
localhost:5001
```

---

# Property 4: Path

Gets the requested URL path.

```csharp
string path =
    HttpContext.Request.Path;
```

Output

```text
/api/products
```

---

# Property 5: QueryString

Gets the complete query string.

URL

```text
https://localhost:5001/products?id=10&name=Laptop
```

Code

```csharp
string query =
    HttpContext.Request.QueryString.Value;
```

Output

```text
?id=10&name=Laptop
```

---

# Property 6: Query

Gets individual query parameters.

URL

```text
https://localhost:5001/products?id=10&name=Laptop
```

Code

```csharp
string id =
    HttpContext.Request.Query["id"];

string name =
    HttpContext.Request.Query["name"];
```

Output

```text
10
Laptop
```

---

# Property 7: Headers

Gets all request headers.

```csharp
foreach (var header in HttpContext.Request.Headers)
{
    Console.WriteLine(
        $"{header.Key} : {header.Value}");
}
```

Example Output

```text
User-Agent : Mozilla/5.0
Accept : application/json
```

---

# Property 8: Cookies

Gets cookies sent by the client.

```csharp
string theme =
    HttpContext.Request.Cookies["Theme"];
```

Output

```text
Dark
```

---

# Property 9: Form

Gets submitted form data.

```csharp
string username =
    HttpContext.Request.Form["Username"];
```

Example

```text
Username = John
```

---

# Property 10: Body

Gets the request body.

```csharp
Stream body =
    HttpContext.Request.Body;
```

The body may contain:

- JSON
- XML
- Text
- Binary Data

---

# Property 11: RouteValues

Gets values from the route.

Route

```text
/products/10
```

Code

```csharp
string id =
    HttpContext.Request.RouteValues["id"]?.ToString();
```

Output

```text
10
```

---

# Property 12: ContentType

Gets the request content type.

```csharp
string type =
    HttpContext.Request.ContentType;
```

Example Output

```text
application/json
```

---

# Property 13: ContentLength

Gets the size of the request body.

```csharp
long? length =
    HttpContext.Request.ContentLength;
```

Output

```text
256
```

(Bytes)

---

# Example 1 - Get Request Method

```csharp
public IActionResult Index()
{
    string method =
        HttpContext.Request.Method;

    return Content(method);
}
```

---

# Example 2 - Read Query String

URL

```text
/products?id=100
```

Code

```csharp
public IActionResult Index()
{
    string id =
        HttpContext.Request.Query["id"];

    return Content(id);
}
```

Output

```text
100
```

---

# Example 3 - Read Header

```csharp
public IActionResult Index()
{
    string userAgent =
        HttpContext.Request.Headers["User-Agent"];

    return Content(userAgent);
}
```

---

# Example 4 - Read Cookie

```csharp
public IActionResult Index()
{
    string theme =
        HttpContext.Request.Cookies["Theme"];

    return Content(theme);
}
```

---

# HttpRequest Structure

```text
HttpRequest
│
├── Method
├── Scheme
├── Host
├── Path
├── QueryString
├── Query
├── Headers
├── Cookies
├── Form
├── Body
├── RouteValues
├── ContentType
└── ContentLength
```

---

# Advantages

- Provides complete information about the incoming request.
- Easy access to headers, cookies, and query parameters.
- Supports reading request body and form data.
- Used throughout ASP.NET Core applications.

---

# Limitations

- Represents only the incoming request.
- Exists only during the current HTTP request.
- The request body stream may only be read once unless buffering is enabled.

---

# Best Practices

- Validate all user input.
- Check for null values before accessing request data.
- Avoid reading the request body multiple times unless request buffering is enabled.
- Use model binding for complex request data whenever possible.
- Use HTTPS to protect sensitive request information.

---

# Interview Questions

### 1. What is HttpRequest?

`HttpRequest` represents the incoming HTTP request sent by the client.

---

### 2. How do you access HttpRequest?

```csharp
HttpRequest request =
    HttpContext.Request;
```

---

### 3. Which property returns the HTTP method?

```csharp
HttpContext.Request.Method
```

---

### 4. Which property contains query parameters?

```csharp
HttpContext.Request.Query
```

---

### 5. Which property contains request headers?

```csharp
HttpContext.Request.Headers
```

---

### 6. Which property contains cookies?

```csharp
HttpContext.Request.Cookies
```

---

### 7. Which property returns the request body?

```csharp
HttpContext.Request.Body
```

---

# HttpRequest vs HttpContext

| HttpRequest | HttpContext |
|-------------|-------------|
| Represents only the incoming request | Represents the complete HTTP request-response cycle |
| Contains request information | Contains Request, Response, User, Session, Connection, and more |
| Accessed using `HttpContext.Request` | Created automatically for every HTTP request |

---
