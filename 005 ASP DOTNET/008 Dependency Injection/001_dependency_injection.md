# Dependency Injection (DI) Basics

# What is Dependency Injection?

Dependency Injection (DI) is a design pattern used to provide objects automatically.

ASP.NET Core creates and injects required objects automatically.

# Simple Meaning

```text
DI = Giving required object automatically
```

# Example Without DI

```cs
public class EmployeeController
{
    EmployeeService service = new EmployeeService();
}
```

Problem:
- Tight coupling
- Hard to manage

---

# Example With DI

```cs
public class EmployeeController
{
    private readonly EmployeeService _service;

    public EmployeeController(EmployeeService service)
    {
        _service = service;
    }
}
```

ASP.NET Core automatically gives object.

# Constructor Injection

Dependencies are injected through constructor.

# Example

```cs
public class EmployeeController
{
    private readonly IEmployeeService _service;

    public EmployeeController(IEmployeeService service)
    {
        _service = service;
    }
}
```

---

# Flow

```text
Controller Created
        ↓
ASP.NET Core Checks Constructor
        ↓
Creates Service Object
        ↓
Injects Into Constructor
```

---

# Service Registration

Services must be registered in `Program.cs`.

**Example:**

```cs
builder.Services.AddScoped<IEmployeeService, EmployeeService>();
```

# Meaning

```text
Interface → Implementation
```

---

# IServiceCollection

```cs
builder.Services
```
# Purpose

Used to register services into DI container.

# Example

```cs
builder.Services.AddScoped<IEmployeeService, EmployeeService>();
```

# Simple Meaning

```text
IServiceCollection = Service Registration List
```

# Service Provider

```cs
app.Services
```

# Purpose

Used to get registered services.

---

Example 1:

```cs
var db = app.Services.GetRequiredService<AppDbContext>();
```

Example 2:
```cs
using var scope = app.Services.CreateScope();

var db = scope.ServiceProvider.GetRequiredService<AppDbContext>();

db.Database.Migrate();
```

# Simple Meaning

```text
Service Provider = Service Giver
```

---

# COMPLETE DI FLOW

```text
Register Service
      ↓
Stored in DI Container
      ↓
Controller Requests Service
      ↓
ASP.NET Core Creates Object
      ↓
Injects Automatically
```

---

# SIMPLE REAL-LIFE ANALOGY

| ASP.NET Core DI | Real Life |
|---|---|
| DI Container | Service center |
| Service Registration | Register worker |
| Constructor Injection | Worker assigned automatically |
| Singleton | One manager for company |
| Scoped | One worker per customer |
| Transient | New temporary worker every time |