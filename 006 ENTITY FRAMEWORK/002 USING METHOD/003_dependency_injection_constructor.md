# Constructor Injection
- Most common DI method.

Used in:
- Controllers
- Services
- Repositories
- Business Classes


## Registration

```cs
builder.Services.AddDbContext<AppDbContext>();
```

## Constructor Injection

**Old Version C#:**
```cs
public class EmployeeService
{
    private readonly AppDbContext _context;

    public EmployeeService(AppDbContext context)
    {
        _context = context;
    }
}
```

**New Version C#:**
```cs
public class EmployeeService
{
    public EmployeeService(AppDbContext context)
    {
        private readonly AppDbContext _context = context;
    }
}
```


## Usage

```cs
public List<Employee> GetAll()
{
    return _context.Employees.ToList();
}
```

---

## Controller Example

```cs
public class EmployeeController: ControllerBase
{
    private readonly AppDbContext _context;

    public EmployeeController(AppDbContext context)
    {
        _context = context;
    }

    [HttpGet]
    public IActionResult Get()
    {
        return Ok(_context.Employees.ToList());
    }
}
```

---

## Flow

```text
Request
    ↓
Controller Created
    ↓
ASP.NET Core Creates AppDbContext
    ↓
Inject Into Constructor
    ↓
Use Object
```


```text

Constructor Injection

Used In
    ↓
Controller
Service
Repository

Most Common
    ↓
Constructor Injection
```


---

# Comparison

| CreateScope() | Constructor Injection |
|--------------|----------------------|
| Manual Resolve From DI | Automatic Injection |
| Program.cs | Controller |
| Worker Service | Service Class |
| Background Service | Repository |
| Less Common | Most Common |
