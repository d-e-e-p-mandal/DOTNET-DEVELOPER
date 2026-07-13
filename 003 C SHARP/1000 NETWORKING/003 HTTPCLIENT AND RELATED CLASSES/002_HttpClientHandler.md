
# HttpClientHandler

- `HttpClientHandler` is a class in .NET that controls **how `HttpClient` sends HTTP requests** and **receives HTTP responses**.
- It acts as a configuration layer between `HttpClient` and the web server.

- If you want to change the default behavior, you create your own `HttpClientHandler`.
- **`HttpClientHandler` allows you to configure things like:**
      - Cookies
      - Automatic redirects
      - Proxy server
      - SSL certificate validation
      - Client certificates
      - Windows authentication
      - Use Windows credentials
      - Compression


### Namespace
```csharp
using System.Net.Http;
```

**How It Works:**
```text
Create HttpClientHandler
          │
          ▼
Configure Handler
          │
          ▼
Pass Handler to HttpClient
          │
          ▼
Send Request
          │
          ▼
Receive Response
```
- `HttpClient` sends the request.
- `HttpClientHandler` decides **how the request should be sent**.

---

## Create a HttpClientHandler

```csharp
HttpClientHandler handler = new HttpClientHandler();

HttpClient client = new HttpClient(handler);
```

## Common Properties

| Property | Description |
|----------|-------------|
| AllowAutoRedirect | Automatically follows redirect responses |
| UseCookies | Enables or disables cookies |
| CookieContainer | Stores cookies |
| Credentials | Sets authentication credentials |
| Proxy | Configures a proxy server |
| UseProxy | Enables or disables proxy |
| AutomaticDecompression | Automatically decompresses responses |
| ClientCertificates | Adds client certificates |
| ServerCertificateCustomValidationCallback | Custom SSL certificate validation |

---

## Property 1: AllowAutoRedirect
- By default, redirects are followed automatically.

**Example:**
```csharp
HttpClientHandler handler = new HttpClientHandler();
handler.AllowAutoRedirect = false;
HttpClient client = new HttpClient(handler);
```

- Now the client will **not** automatically follow redirects.

---

## Property 2: UseCookies
- By Default value : true


**Enable cookies:**
```csharp
HttpClientHandler handler = new HttpClientHandler();
handler.UseCookies = true;
```

**Disable cookies:**
```csharp
handler.UseCookies = false;
```

---

## Property 3: CookieContainer
- Store cookies manually.

```csharp
HttpClientHandler handler = new HttpClientHandler();

handler.CookieContainer = new CookieContainer();
```

---

## Property 4: Credentials: UseDefaultCredentials 

Use Windows credentials.

```csharp
HttpClientHandler handler = new HttpClientHandler();

handler.UseDefaultCredentials = true;
```
- Default credentials are the Windows account credentials of the user running the application.
- For example, if you are logged into Windows as:
      - Username : deep
      - Domain   : COMPANY
then these credentials are automatically sent to servers that support Windows Authentication.

*Authenticate:* You do not need to write:
```json
Username = "deep";
Password = "...";
```

---

# Property 5: Proxy

Use a proxy server.

```csharp
HttpClientHandler handler = new HttpClientHandler();

handler.Proxy = new WebProxy("http://proxy.example.com:8080");

handler.UseProxy = true;
```

---

# Property 6: AutomaticDecompression

Automatically decompress compressed responses.

```csharp
HttpClientHandler handler = new HttpClientHandler();

handler.AutomaticDecompression = System.Net.DecompressionMethods.GZip | System.Net.DecompressionMethods.Deflate;
```

---

# Property 7: Ignore SSL Certificate (Development Only)

Sometimes developers use self-signed certificates during development.

```csharp
HttpClientHandler handler = new HttpClientHandler();

handler.ServerCertificateCustomValidationCallback =
    HttpClientHandler.DangerousAcceptAnyServerCertificateValidator;
```

- ⚠️ **Never use this in `production`.**

---



# Property 8: Enable Compression

```csharp
HttpClientHandler handler = new HttpClientHandler();

handler.AutomaticDecompression = System.Net.DecompressionMethods.All;

HttpClient client = new HttpClient(handler);
```


---
---

# Advantages

- Easy to configure HTTP behavior
- Supports cookies
- Supports authentication
- Supports proxies
- Supports SSL configuration
- Supports automatic decompression
- Gives more control over HTTP requests

---

# Limitations

- Configuration applies to the associated `HttpClient`
- SSL validation should not be disabled in production
- Incorrect configuration can affect all requests made through the client

---

# Best Practices

- Reuse the same `HttpClientHandler` when appropriate.
- Configure the handler before creating `HttpClient`.
- Enable compression to reduce network usage.
- Use cookies only when required.
- Do not disable SSL certificate validation in production.
- Dispose `HttpClient` and `HttpClientHandler` properly if they are not managed by dependency injection.

---

## Interview Questions
### 1. What is HttpClientHandler?
- It is a class that controls how `HttpClient` sends HTTP requests and receives HTTP responses.

---

### 2. Why is HttpClientHandler used?
- It is used to customize the behavior of `HttpClient`, such as cookies, redirects, proxies, authentication, and SSL settings.

---

### 3. Can HttpClient work without HttpClientHandler?
- Yes. `HttpClient` creates and uses a default handler automatically if one is not provided.

---

### 4. Can one HttpClientHandler be shared?
- Yes, it can be shared when the same configuration is appropriate for multiple requests.

---

### 5. Should SSL certificate validation be disabled in production?
- No. It should only be disabled temporarily during development or testing with trusted self-signed certificates.

---