# 🔹 Session & State Management in ASP.NET Core

---

# What is State Management?

HTTP is stateless.

This means:
- Server does NOT remember previous requests automatically.

---

# Example

---

# Request 1

```text
User Login
```

---

# Request 2

```text
Open Dashboard
```

Server forgets previous request.

---

# Problem

How to remember:
- User login
- Shopping cart
- User preferences

---

# Solution

```text
State Management
```

---

# Simple Meaning

```text
State Management
    ↓
Store User Data Between Requests
```

---

# Types of State Management

- Session
- Cookies
- TempData
- Cache
- Distributed Cache

---

# 1. Session

---

# What is Session?

Session stores user data on server temporarily.

Each user gets unique session.

---

# Purpose

Used for:
- Login session
- Shopping cart
- Temporary user data

---

# Session Flow

```text
User Request
      ↓
Session Created
      ↓
Session ID Stored In Cookie
      ↓
Server Stores User Data
```

---

# Session Storage

Session data stored on:
- Server memory

---

# Configure Session

## Program.cs

```cs
builder.Services.AddSession();

var app = builder.Build();

app.UseSession();
```

---

# IMPORTANT

Both required:
- AddSession()
- UseSession()

---

# Store Session Data

```cs
HttpContext.Session.SetString(
    "Name",
    "Deep");
```

---

# Explanation

---

# "Name"

Session key.

---

# "Deep"

Session value.

---

# Read Session Data

```cs
var name =
    HttpContext.Session
        .GetString("Name");
```

---

# Output

```text
Deep
```

---

# Remove Session

```cs
HttpContext.Session.Remove("Name");
```

---

# Clear All Session

```cs
HttpContext.Session.Clear();
```

---

# Session Features

- Server-side storage
- Secure
- Temporary data

---

# Session Timeout

```cs
builder.Services.AddSession(options =>
{
    options.IdleTimeout =
        TimeSpan.FromMinutes(20);
});
```

---

# Meaning

Session expires after:
- 20 minutes

---

# Session Use Cases

- Shopping cart
- Logged-in user
- OTP verification

---

# Simple Meaning

```text
Session
    ↓
Temporary User Data On Server
```

---

# 2. Cookies

---

# What are Cookies?

Cookies store small data in browser.

---

# Purpose

Used for:
- Login remember
- Preferences
- Tracking

---

# Cookie Flow

```text
Server Creates Cookie
      ↓
Browser Stores Cookie
      ↓
Browser Sends Cookie With Request
```

---

# Create Cookie

```cs
Response.Cookies.Append(
    "Name",
    "Deep");
```

---

# Read Cookie

```cs
var name =
    Request.Cookies["Name"];
```

---

# Output

```text
Deep
```

---

# Delete Cookie

```cs
Response.Cookies.Delete("Name");
```

---

# Cookie Features

- Stored in browser
- Small size
- Sent automatically

---

# Cookie Options

```cs
Response.Cookies.Append(
    "Name",
    "Deep",
    new CookieOptions
    {
        Expires =
            DateTime.Now.AddDays(1)
    });
```

---

# Meaning

Cookie expires after:
- 1 day

---

# Cookie Types

| Type | Purpose |
|---|---|
| Session Cookie | Temporary |
| Persistent Cookie | Long-term |

---

# Cookies vs Session

| Cookies | Session |
|---|---|
| Browser storage | Server storage |
| Less secure | More secure |
| Small data | Larger data |

---

# Simple Meaning

```text
Cookies
    ↓
Small Browser Storage
```

---

# 3. TempData

---

# What is TempData?

TempData stores data temporarily between requests.

Mostly used in:
- MVC

---

# Purpose

Used for:
- Success messages
- Redirect messages

---

# TempData Flow

```text
Controller 1
      ↓
Redirect
      ↓
Controller 2
      ↓
Read TempData
```

---

# Store TempData

```cs
TempData["Message"] =
    "Data Saved";
```

---

# Read TempData

```cs
var msg =
    TempData["Message"];
```

---

# Output

```text
Data Saved
```

---

# IMPORTANT

TempData removed automatically after reading.

---

# Keep TempData

```cs
TempData.Keep();
```

---

# TempData Features

- Temporary storage
- Redirect support
- Auto remove

---

# TempData Internally Uses

- Session
or
- Cookies

---

# Common Use

```text
"Record Saved Successfully"
```

after redirect.

---

# Simple Meaning

```text
TempData
    ↓
Temporary Redirect Data
```

---

# 4. Cache

---

# What is Cache?

Cache stores frequently used data for faster access.

---

# Purpose

Used for:
- Improve performance
- Reduce database calls

---

# Cache Flow

```text
Request Data
      ↓
Check Cache
   ↓         ↓
Exists      Not Exists
 ↓             ↓
Return      Get From DB
Fast Data   Store In Cache
```

---

# Types of Cache

- In-Memory Cache
- Distributed Cache

---

# In-Memory Cache

Stored in:
- Server memory

---

# Configure Cache

```cs
builder.Services.AddMemoryCache();
```

---

# Inject IMemoryCache

```cs
private readonly IMemoryCache
    _cache;
```

---

# Store Cache

```cs
_cache.Set(
    "Name",
    "Deep");
```

---

# Read Cache

```cs
var name =
    _cache.Get<string>("Name");
```

---

# Cache Expiration

```cs
_cache.Set(
    "Name",
    "Deep",
    TimeSpan.FromMinutes(10));
```

---

# Meaning

Cache expires after:
- 10 minutes

---

# Cache Benefits

- Faster response
- Better performance
- Less DB load

---

# Cache Drawback

Lost when:
- Server restarts

---

# Simple Meaning

```text
Cache
    ↓
Fast Temporary Memory
```

---

# 5. Distributed Cache

---

# What is Distributed Cache?

Cache shared across multiple servers.

---

# Used In

- Large applications
- Cloud systems
- Load balanced systems

---

# Example Technologies

- Redis
- SQL Server Cache

---

# Why Needed?

In-memory cache works only:
- On single server

Distributed cache works:
- Across all servers

---

# Configure Redis Cache

```cs
builder.Services
    .AddStackExchangeRedisCache(options =>
{
    options.Configuration =
        "localhost:6379";
});
```

---

# Inject IDistributedCache

```cs
private readonly
    IDistributedCache _cache;
```

---

# Store Data

```cs
await _cache.SetStringAsync(
    "Name",
    "Deep");
```

---

# Read Data

```cs
var name =
    await _cache.GetStringAsync(
        "Name");
```

---

# Distributed Cache Features

- Shared cache
- Faster applications
- Scalable systems

---

# Distributed Cache Flow

```text
Application Server 1
        ↓
Redis Cache
        ↑
Application Server 2
```

---

# Cache vs Distributed Cache

| Cache | Distributed Cache |
|---|---|
| Single server | Multiple servers |
| Faster local access | Shared access |
| Memory based | External storage |

---

# State Management Summary

| Type | Storage |
|---|---|
| Session | Server |
| Cookies | Browser |
| TempData | Session/Cookies |
| Cache | Server Memory |
| Distributed Cache | External Server |

---

# Common Use Cases

| Feature | Usage |
|---|---|
| Session | Shopping cart |
| Cookies | Remember login |
| TempData | Success message |
| Cache | Frequently used data |
| Distributed Cache | Large systems |

---

# Complete State Management Flow

```text
User Request
      ↓
State Management Stores Data
      ↓
Next Request
      ↓
Data Retrieved
```

---

# Real-Life Analogy

| ASP.NET Core | Real Life |
|---|---|
| Session | Temporary Locker |
| Cookies | Pocket Note |
| TempData | One-Time Message |
| Cache | Fast Access Shelf |
| Distributed Cache | Shared Warehouse |

---

# SIMPLE UNDERSTANDING

```text
Session
    ↓
Temporary Server Storage

Cookies
    ↓
Browser Storage

TempData
    ↓
One-Time Data

Cache
    ↓
Fast Memory Storage

Distributed Cache
    ↓
Shared Fast Storage
```