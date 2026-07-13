
## Validation Techniques

## Automatic Validation 

When using [ApiController]
```cs
[ApiController]
public class EmployeeController : ControllerBase
```
If data is invalid → automatic error response

### Internal Working :

```
Client → Send JSON
   ↓
Model Binding (JSON → Employee object)
   ↓
Validation (DataAnnotations checked)
   ↓
If invalid → ASP.NET stops execution 
   ↓
Returns automatic 400 response
```

1. Model (with validation rules)
```cs
using System.ComponentModel.DataAnnotations;

public class Employee
{
    [Required]              // must be provided
    public string Name { get; set; }

    [Range(1000, 100000)]   // must be in range
    public int Salary { get; set; }
}
```

Controller :
```cs
[ApiController]   // enables automatic validation
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
    [HttpPost]
    public IActionResult Create(Employee emp)
    {
        // ❌ No need to write:
        // if (!ModelState.IsValid) ...

        return Ok(emp);
    }
}
```

```json
{
  "errors": {
    "Name": ["The Name field is required."],
    "Salary": ["The field Salary must be between 1000 and 100000."]
  },
  "title": "One or more validation errors occurred.",
  "status": 400
}
```
 ------------


## Manual Validation
```cs
[HttpPost]
public IActionResult Create(Employee emp)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }
    return Ok(emp);
}
```

-----

## Custom Validation

Create your own validation
```cs
public class CustomSalary : ValidationAttribute
{
    protected override ValidationResult IsValid(object value, ValidationContext context)
    {
        if ((int)value < 5000)
            return new ValidationResult("Salary too low");
        return ValidationResult.Success;
    }
}
```
**Use it :**
```cs
[CustomSalary]
public int Salary { get; set; }
```

----

Full Flow : Client → Send Data → Model Binding → Validation → Controller
