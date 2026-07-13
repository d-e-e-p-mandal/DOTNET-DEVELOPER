
# HTTP METHOD ATTRIBUTES

### [HttpGet]
- Fetch data
```cs
[HttpGet]
public IActionResult Get()
```

### [HttpPost]
- Create data
```cs
[HttpPost]
public IActionResult Create(Employee emp)
```

### [HttpPut]
- Update full data
```cs
[HttpPut("{id}")]
public IActionResult Update(int id, Employee emp)
```

### [HttpDelete]
- Delete data
```cs
[HttpDelete("{id}")]
public IActionResult Delete(int id)
```

### [HttpPatch]
- Partial update
```cs
[HttpPatch("{id}")]
public IActionResult Patch(int id, Employee emp)
```


**CONTROLLER + ROUTING INTERNAL FLOW**

```
Client Request
   ↓
Routing System ([Route])
   ↓
Controller Selected
   ↓
Action Method ([HttpGet])
   ↓
Model Binding
   ↓
Return Result (Ok, NotFound)
   ↓
HTTP Response
```

**CONTROLLER EXAMPLE :**
```cs
[ApiController]
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
    [HttpGet("{id}")]
    public IActionResult Get(int id)
    {
        if (id <= 0)
            return BadRequest("Invalid ID");
        return Ok(new { Id = id, Name = "Deep" });
    }
    [HttpPost]
    public IActionResult Create(Employee emp)
    {
        return CreatedAtAction(nameof(Get), new { id = 1 }, emp);
    }
    [HttpDelete("{id}")]
    public IActionResult Delete(int id)
    {
        return NoContent();
    }
}
```

------------

# Routing In HTTP Method :

```cs
[HttpGet("employee")]
public IActionResult Get()
```

### ROUTE PARAMETERS
```cs
[HttpGet("{id}")]
public IActionResult Get(int id)
```

URL : /api/employee/5
> id = 5