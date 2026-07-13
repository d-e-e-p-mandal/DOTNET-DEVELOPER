
### How to Use:
- Write One by One.
```cs
[Table("Employees")]
public class Employee
{
    [Key]
    [StringLength(50)]
    public string Id { get; set; }
}
```
 
- Write together.
```cs
[Table("Employees")]
public class Employee
{
    [key, StringLength(50)]
    public string Id { get; set; }
}
```



### 8. REQUEST MODEL (INPUT FROM CLIENT)

- Used in API (POST / PUT)
```cs
public class EmployeeRequest
{
    [Required]                         // must come from client
    public string Name { get; set; }
    [Range(1000, 100000)]             // validate input
    public int Salary { get; set; }
    [BindNever]                       // ignore even if client sends
    public int InternalId { get; set; }
}
```


- Controller (Request Handling)
```cs
[HttpPost]
public IActionResult Create(EmployeeRequest req)
{
    // Automatic validation with [ApiController]
    return Ok(req); // valid data comes here
}
```


### 9. RESPONSE MODEL (OUTPUT TO CLIENT)

- Used to control what client sees
```cs
public class EmployeeResponse
{
    public int Id { get; set; }
    [JsonPropertyName("employee_name")]  
    public string Name { get; set; }
    public int Salary { get; set; }
    [JsonIgnore]   // hide sensitive data
    public string InternalCode { get; set; }
}
```


### 10. FULL MODEL (COMBINED EXAMPLE)
```cs
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
using System.Text.Json.Serialization;
[Table("Employees")]
public class Employee
{
    [Key]
    public int Id { get; set; }
    [Required]
    [JsonPropertyName("employee_name")]
    public string Name { get; set; }
    [Range(1000, 100000)]
    public int Salary { get; set; }
    [JsonIgnore]        // not sent to client
    public string InternalCode { get; set; }
    [NotMapped]         // not saved in DB
    public string TempData { get; set; }
}
```


### 11. REQUEST vs RESPONSE In Attrubute

| Feature            | Request | Response |
|------------------|--------|----------|
| Validation        | ✔      | x        |
| DataAnnotations   | ✔      | x        |
| JsonPropertyName  | ✔      | ✔        |
| JsonIgnore        | ✔      | ✔        |
| BindNever         | ✔      | x        |

```
Client → Request Model → Model Binding → Validation  → Controller → Entity → Response Model → JSON Output
```