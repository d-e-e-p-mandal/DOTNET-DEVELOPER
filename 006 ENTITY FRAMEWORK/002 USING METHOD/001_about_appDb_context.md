# DbContext in ASP.NET Core Web API

---

# What is DbContext?

`DbContext` is the main EF Core class.

It is used to communicate with the database.

It performs:

- Read Data
- Insert Data
- Update Data
- Delete Data

Example

```csharp
public class AppDbContext : DbContext
{
    public DbSet<Employee> Employees { get; set; }
}
```

---

# Register DbContext

Register it in `Program.cs`.

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

Why?

- Register `DbContext`
- Connect to SQL Server
- Enable Dependency Injection (DI)

---

# DbContext Lifetime

By default,

```text
DbContext = Scoped
```

This means one `DbContext` object is created for **one HTTP request**.

---

# How Scope Works in Web API

When a request comes,

```text
User Request

↓

ASP.NET Core

↓

Create Scope

↓

Create Controller

↓

Create DbContext

↓

Execute Action

↓

Return Response

↓

Dispose DbContext

↓

Dispose Scope
```

You do **not** create the scope yourself.

ASP.NET Core creates it automatically.

---

# Controller Example

```csharp
public class EmployeeController : ControllerBase
{
    private readonly AppDbContext _context;

    public EmployeeController(AppDbContext context)
    {
        _context = context;
    }
}
```

Why does this work?

Because ASP.NET Core already created a **Scope** for this request.

---

# One Request = One DbContext

Request 1

```text
Scope 1

↓

DbContext 1
```

Request 2

```text
Scope 2

↓

DbContext 2
```

Request 3

```text
Scope 3

↓

DbContext 3
```

Each request gets a **new DbContext**.

---

# Why Scoped?

Each request works independently.

Benefits:

- Safe for multiple users
- No shared data
- Thread-safe
- Automatic cleanup
- Better performance

---

# What Happens After Response?

After the response is sent,

```text
Response Sent

↓

Dispose DbContext

↓

Dispose Scope

↓

Close Database Connection
```

Everything is cleaned automatically.

---

# Why Not Singleton?

If one `DbContext` was shared by everyone,

```text
User 1

↓

Same DbContext

↑

User 2

↑

User 3
```

Problems:

- Thread conflicts
- Wrong entity tracking
- Memory growth
- Connection issues

So **DbContext should not be Singleton**.

---

# Typical Web API Flow

```text
HTTP Request

↓

ASP.NET Core

↓

Create Scope

↓

Create DbContext

↓

Controller

↓

Read / Insert / Update / Delete

↓

SaveChangesAsync()

↓

Return Response

↓

Dispose DbContext

↓

Dispose Scope
```

---

# Key Points

- `DbContext` is the main EF Core class.
- `DbContext` is **Scoped** by default.
- One HTTP request gets one `DbContext`.
- ASP.NET Core automatically creates the scope.
- You can inject `DbContext` directly into Controllers.
- After the request ends, `DbContext` is automatically disposed.
- No need to call `CreateScope()` in Web API.

---

# Web API vs Background Service

| Web API | Background Service |
|---------|--------------------|
| HTTP request exists | No HTTP request |
| Scope created automatically | You must create the scope |
| Inject `DbContext` directly | Use `IServiceScopeFactory` |
| One `DbContext` per request | One `DbContext` per created scope |

---

# Simple Interview Questions

### Why is DbContext Scoped?

Because each HTTP request should use its own `DbContext`.

---

### Who creates the Scope in Web API?

ASP.NET Core automatically creates the scope for every HTTP request.

---

### Do we call `CreateScope()` in Web API?

**No.**

ASP.NET Core creates and disposes the scope automatically.

---

### When do we call `CreateScope()`?

Only in services that do not have an automatic scope, such as:

- Background Service (`BackgroundService`)
- Worker Service
- Hosted Service