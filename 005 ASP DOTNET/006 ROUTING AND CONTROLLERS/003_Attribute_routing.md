
# Attribute Routing

**Definition :**
- Attribute Routing is a routing technique in ASP.NET Core where routes are defined directly on controllers and action methods using attributes.

- It gives full control over URL structure.

### Why Attribute Routing?

- In Conventional Routing, routes are defined in one place (Program.cs)
- In Attribute Routing, routes are defined where they are used

✔ More flexible
✔ More readable
✔ Best for APIs

#### [ApiController] Attribute
```cs
[ApiController]
```
Enables:
	•	Automatic model validation
	•	Binding from body/query automatically
	•	Cleaner API behavior

---

### Basic Syntax
```cs
[ApiController]
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok("Data");
    }
}
```

**Explanation : [Route("api/[controller]")]**
	•	[controller] → replaced by controller name
	•	EmployeeController → employee

Final base URL: /api/employee


## Http Method : 
**Explanation : [HttpGet]**
	•	HTTP method = GET
	•	Uses base route

Final URL: GET /api/employee

1. Route Parameters

Definition : Pass values through URL

📌 Example
```cs
[HttpGet("{id}")]
public IActionResult GetById(int id)
{
    return Ok(id);
}
```

URL : /api/employee/5
id = 5

2. Multiple Parameters
```cs
[HttpGet("{id}/{name}")]
public IActionResult Get(int id, string name)
```

URL: /api/employee/5/deep

### Combining Route + HTTP Method

- define route inside HTTP method

```cs
[HttpGet("all")]
public IActionResult GetAll()
{
    return Ok("All Employees");
}
```
URL: /api/employee/all

### Controller Level + Action Level Routing

📌 Example
```cs
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
    [HttpGet("all")]
    public IActionResult GetAll()
    {
        return Ok("All Employees");
    }

    [HttpGet("{id}")]
    public IActionResult GetById(int id)
    {
        return Ok(id);
    }
}
```

Method	URL
GET	/api/employee/all
GET	/api/employee/5


#### Optional Parameters
```cs
[HttpGet("{id?}")]
public IActionResult Get(int id = 0)
{
    return Ok(id);
}
```
Works for:
/api/employee
/api/employee/5


#### Route Constraints

- Restrict parameter type
```cs
[HttpGet("{id:int}")]
public IActionResult Get(int id)
```
- Only accepts integer

#### More Constraints
```cs
[HttpGet("{id:int}")]
[HttpGet("{name:alpha}")]
```

Constraint - Meaning
int	integer - only
alpha - letters only
bool - true/false
datetime - date

#### Query String vs Route Parameter

**Route Parameter :** /api/employee/5
**Query String :** /api/employee?id=5

Both Parameter is recieved in function : 
```cs
public IActionResult Get(int id)
```

CRUD Example :
```cs
[ApiController]
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
    // GET: /api/employee
    [HttpGet]
    public IActionResult GetAll()
    {
        return Ok("All Employees");
    }

    // GET: /api/employee/1
    [HttpGet("{id}")]
    public IActionResult GetById(int id)
    {
        return Ok(id);
    }

    // POST: /api/employee
    [HttpPost]
    public IActionResult Create()
    {
        return Ok("Created");
    }

    // PUT: /api/employee/1
    [HttpPut("{id}")]
    public IActionResult Update(int id)
    {
        return Ok($"Updated {id}");
    }

    // PATCH: /api/employee/1
    [HttpPatch("{id}")]
    public IActionResult UpdatePartial(int id)
    {
        return Ok($"Partial Update {id}");
    }

    // DELETE: /api/employee/1
    [HttpDelete("{id}")]
    public IActionResult Delete(int id)
    {
        return Ok($"Deleted {id}");
    }
}
```

⸻

### Advantages

✅ Full control over URL
✅ Easy to understand
✅ Best for REST APIs
✅ No dependency on Program.cs

❌ Disadvantages

❌ More attributes → more code
❌ Hard to manage if not structured properly

⸻
```
Attribute Routing Flow

Client Request
     ↓
Route Attribute Match
     ↓
Controller Selected
     ↓
Action Method Executes
     ↓
Response Returned
```