# Middleware Basics

---

# What is Middleware?

Middleware is a small software component that handles:
- Request
- Response

inside ASP.NET Core application.

---

# Simple Meaning

```text
Middleware = Request/Response Handler
```

---

# Middleware Works Between

```text
Client
   ↕
Middleware
   ↕
Controller
```

---

# Example

When browser sends request:

```text
https://localhost:5001/api/employee
```

Request passes through middleware.

Middleware can:
- Check security
- Check authentication
- Log request
- Redirect HTTPS

---

# Middleware Flow

```text
Browser Request
        ↓
Middleware 1
        ↓
Middleware 2
        ↓
Middleware 3
        ↓
Controller
        ↓
Response
        ↓
Middleware 3
        ↓
Middleware 2
        ↓
Middleware 1
        ↓
Browser
```

---

# Request-Response Pipeline

ASP.NET Core processes requests using pipeline.

Pipeline = Multiple middlewares connected together.

---

# Simple Meaning

```text
Pipeline = Chain of Middlewares
```

---

# Real Flow

```text
Request
  ↓
Authentication Middleware
  ↓
Authorization Middleware
  ↓
Routing Middleware
  ↓
Controller
  ↓
Response
```

---

# Middleware in Program.cs

```cs
app.UseHttpsRedirection();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();
```

---

# Explanation

---

# UseHttpsRedirection()

```cs
app.UseHttpsRedirection();
```

Redirects:
- HTTP → HTTPS

---

# UseAuthentication()

```cs
app.UseAuthentication();
```

Checks:
- User login
- JWT token
- Identity

---

# UseAuthorization()

```cs
app.UseAuthorization();
```

Checks:
- Permissions
- Roles

---

# MapControllers()

```cs
app.MapControllers();
```

Sends request to controllers.

---

# IMPORTANT

Middleware order matters.

---

# Correct Order

```cs
app.UseAuthentication();

app.UseAuthorization();
```

---

# Wrong Order

```cs
app.UseAuthorization();

app.UseAuthentication();
```

May cause errors.

---

# Built-in Middleware Examples

| Middleware | Purpose |
|---|---|
| UseHttpsRedirection | HTTPS redirect |
| UseAuthentication | Login checking |
| UseAuthorization | Permission checking |
| UseStaticFiles | Serve CSS/JS/images |
| UseRouting | Route matching |

---

# Custom Middleware

We can create our own middleware.

---

# Example

```cs
public class LoggingMiddleware
{
    
}
```

---

# Purpose

Custom tasks:
- Logging
- Error handling
- Request tracking

---

# Simple Request Pipeline Example

```text
Browser Request
        ↓
HTTPS Middleware
        ↓
Authentication Middleware
        ↓
Authorization Middleware
        ↓
Routing Middleware
        ↓
Controller
        ↓
Response
```

---

# Real-Life Analogy

| ASP.NET Core | Real Life |
|---|---|
| Middleware | Security checkpoint |
| Request Pipeline | Airport checking process |
| Authentication | ID verification |
| Authorization | Permission checking |
| Controller | Final destination office |

---

# SIMPLE UNDERSTANDING

```text
Middleware = Security Guard

Pipeline = Multiple Guards Standing In Line
```

---

# COMPLETE FLOW

```text
Client Sends Request
        ↓
Request Enters Pipeline
        ↓
Middlewares Process Request
        ↓
Controller Executes
        ↓
Response Generated
        ↓
Response Passes Through Middlewares
        ↓
Client Receives Response
```