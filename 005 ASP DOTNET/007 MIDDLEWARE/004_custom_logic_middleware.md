# Using Own Logic in Custom Middleware

---

# Middleware Can Read

- Query Parameters
- Route Parameters
- Request Body
- Headers
- Cookies

Then apply:
- Custom validation
- Custom security
- Custom rules

---

# 1. Query Parameter Logic

## URL

```text
/api/employee?id=5
```

---

# Middleware

```cs
public async Task Invoke(HttpContext context)
{
    var id =
        context.Request.Query["id"];

    if (id != "5")
    {
        context.Response.StatusCode = 401;

        await context.Response.WriteAsync(
            "Invalid User");

        return;
    }

    await _next(context);
}
```

---

# What Happens?

Reads:

```text
?id=5
```

---

# Custom Logic

```cs
if (id != "5")
```

---

# Valid Request

```text
/api/employee?id=5
```

Allowed.

---

# Invalid Request

```text
/api/employee?id=2
```

Blocked.

---

# 2. Route Parameter Logic

## URL

```text
/api/employee/5
```

---

# Middleware

```cs
public async Task Invoke(HttpContext context)
{
    var id =
        context.Request.RouteValues["id"];

    if (id?.ToString() != "5")
    {
        context.Response.StatusCode = 401;

        await context.Response.WriteAsync(
            "Invalid Route Id");

        return;
    }

    await _next(context);
}
```

---

# Reads Route Value

```text
/api/employee/5
```

Gets:

```text
id = 5
```

---

# 3. Header Logic

## Request Header

```text
SecretKey: ABC123
```

---

# Middleware

```cs
public async Task Invoke(HttpContext context)
{
    var key =
        context.Request.Headers["SecretKey"];

    if (key != "ABC123")
    {
        context.Response.StatusCode = 401;

        await context.Response.WriteAsync(
            "Invalid Key");

        return;
    }

    await _next(context);
}
```

---

# Custom Logic

```cs
if (key != "ABC123")
```

---

# 4. Body Logic

Reading body is more advanced.

---

# Example JSON

```json
{
  "name": "Deep"
}
```

---

# Middleware Example

```cs
public async Task Invoke(HttpContext context)
{
    context.Request.EnableBuffering();

    using var reader =
        new StreamReader(
            context.Request.Body,
            leaveOpen: true);

    var body =
        await reader.ReadToEndAsync();

    context.Request.Body.Position = 0;

    if (!body.Contains("Deep"))
    {
        context.Response.StatusCode = 401;

        await context.Response.WriteAsync(
            "Invalid Body");

        return;
    }

    await _next(context);
}
```

---

# What Happens?

Reads request body.

---

# Custom Logic

```cs
if (!body.Contains("Deep"))
```

---

# 5. IP Address Logic

```cs
var ip =
    context.Connection.RemoteIpAddress;
```

---

# Example

```cs
if (ip.ToString() != "127.0.0.1")
```

---

# Purpose

Allow only specific IPs.

---

# 6. Time-Based Logic

```cs
if (DateTime.Now.Hour >= 22)
```

---

# Purpose

Block requests after 10 PM.

---

# 7. HTTP Method Logic

```cs
if (context.Request.Method != "GET")
```

---

# Purpose

Allow only GET requests.

---

# 8. Path-Based Logic

```cs
if (context.Request.Path
      == "/api/admin")
```

---

# Purpose

Apply rules for specific routes.

---

# MOST IMPORTANT THING

Custom middleware means:

```text
YOU decide rules
```

---

# ASP.NET Core Gives

- Request
- Response
- HttpContext

---

# YOU Add

- Validation
- Conditions
- Security
- Business Rules

---

# COMPLETE FLOW

```text
Request Comes
      ↓
Middleware Reads Data
(Query/Route/Header/Body)
      ↓
Your Custom Logic Runs
      ↓
Valid ?
   ↓        ↓
 YES       NO
 ↓          ↓
Next       Return Error
Middleware
```

---

# SIMPLE UNDERSTANDING

| Middleware Reads | Example |
|---|---|
| Query | ?id=5 |
| Route | /employee/5 |
| Header | SecretKey |
| Body | JSON Data |
| Method | GET/POST |
| IP | Client Address |

---

# Real-Life Analogy

| Middleware | Real Life |
|---|---|
| Query Check | Ticket checking |
| Header Check | Secret passcode |
| Route Check | Room number |
| Body Check | Form verification |
| Custom Logic | Company rules |