# HttpResponseMessage

- `HttpResponseMessage` is a class in .NET that represents an **HTTP response** received from a web server.
- It contains all the information returned by the server after an HTTP request is sent.

This information includes:
- Status Code
- Response Headers
- Response Body (Content)
- HTTP Version
- Success Status

### Namespace

```csharp
using System.Net.Http;
```

### Response Structure

```text
HttpResponseMessage
│
├── StatusCode
├── IsSuccessStatusCode
├── Headers
├── Content
└── Version
```


**Why Do We Need HttpResponseMessage?**
- When an HTTP request is sent, the server returns a response.

`HttpResponseMessage` stores that response so that you can:
- Check whether the request was successful.
- Read the returned data.
- Read response headers.
- Check the HTTP status code.
- Read the HTTP version.

---

# How It Works

```text
Application
      │
      ▼
HttpClient
      │
      ▼
Web Server
      │
      ▼
HttpResponseMessage
      │
      ▼
Application
```

The server sends an HTTP response.

`HttpResponseMessage` stores that response.

---

# Get an HttpResponseMessage

`HttpClient` returns an `HttpResponseMessage`.

```csharp
HttpClient client = new HttpClient();

HttpResponseMessage response = await client.GetAsync("https://example.com/api/users");
```


**Common Properties:**
| Property | Description |
|----------|-------------|
| StatusCode | HTTP status code returned by the server |
| IsSuccessStatusCode | Indicates whether the request was successful |
| Headers | Response headers |
| Content | Response body |
| Version | HTTP version |


**Common Status Codes:**
| Status Code | Meaning |
|-------------|---------|
| 200 OK | Request successful |
| 201 Created | Resource created successfully |
| 204 No Content | No response body |
| 400 Bad Request | Invalid request |
| 401 Unauthorized | Authentication required |
| 403 Forbidden | Access denied |
| 404 Not Found | Resource not found |
| 500 Internal Server Error | Server error |


### Property 1: StatusCode
- Returns the HTTP status code.

```csharp
Console.WriteLine(response.StatusCode);
```
**Example Output** OK


### Property 2: IsSuccessStatusCode

- Returns `true` if the status code is between **200 and 299**.

```csharp
if (response.IsSuccessStatusCode)
{
    Console.WriteLine("Success");
}
```

#### EnsureSuccessCode:








### Property 3: Headers
- Reads response headers.

```csharp
HttpClient client = new HttpClient();

HttpResponseMessage response =
    await client.GetAsync(
        "https://example.com/api/users");

foreach (var header in response.Headers)
{
    Console.WriteLine(
        $"{header.Key} : {string.Join(", ", header.Value)}");
}
```

---

### Property 4: Content

The response body is stored in the `Content` property.

To read it as a string:

```csharp
string data = await response.Content.ReadAsStringAsync();

Console.WriteLine(data);
```

**Output**
```json
[
  {
    "id": 1,
    "name": "John"
  }
]
```

---

### Property 5: Version
- Returns the HTTP protocol version.

```csharp
Console.WriteLine(response.Version);
```

Example Output

```text
2.0
```

---





---

# Advantages

- Stores the complete HTTP response.
- Allows checking the status code.
- Allows reading response data.
- Provides access to response headers.
- Supports HTTP version information.

---

# Limitations

- It only represents the response; it does not send requests.
- The response body must be read separately from the `Content` property.
- It should be disposed when no longer needed if not managed automatically.

---

# When Should You Use HttpResponseMessage?

Use `HttpResponseMessage` when you need to:

- Check the HTTP status code.
- Verify whether the request succeeded.
- Read response headers.
- Read the response body.
- Access HTTP version information.

---

# Best Practices

- Always check `IsSuccessStatusCode` before processing the response.
- Read the response body only when needed.
- Handle unsuccessful responses appropriately.
- Dispose of the response when it is no longer required.
- Use asynchronous methods when reading the response content.

---

# Interview Questions

### 1. What is HttpResponseMessage?

`HttpResponseMessage` represents the HTTP response returned by a web server.

---

### 2. What information does HttpResponseMessage contain?

It contains:

- Status Code
- Success Status
- Headers
- Response Body (Content)
- HTTP Version

---

### 3. How do you check whether a request was successful?

Using the `IsSuccessStatusCode` property.

```csharp
if (response.IsSuccessStatusCode)
{
    Console.WriteLine("Success");
}
```

---

### 4. How do you read the response body?

```csharp
string data =
    await response.Content.ReadAsStringAsync();
```

---

### 5. Which property contains the response body?

The `Content` property.

---

# HttpRequestMessage vs HttpResponseMessage

| HttpRequestMessage | HttpResponseMessage |
|--------------------|---------------------|
| Represents an HTTP request | Represents an HTTP response |
| Sent by the client | Returned by the server |
| Contains request method, URL, headers, and body | Contains status code, headers, response body, and HTTP version |
| Sent using `HttpClient.SendAsync()` | Returned by `HttpClient` after sending a request |

---
