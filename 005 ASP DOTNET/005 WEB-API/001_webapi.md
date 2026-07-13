
# WEB API (ASP.NET CORE)

# Introduction to Web API

**Definition :** Web API is used to Send and receive data between client and server (mostly JSON)

**Example :** Mobile app / React app ↔ Web API ↔ Database

**Simple Flow :** Client → API → Database → API → Client


### RESTful Services

**Definition :** REST = Standard way to build APIs using HTTP

Rules of REST
- Use proper HTTP methods
- Use URL for resources
- Stateless (no memory of previous request)

**Example URL :** GET /api/employees

### HTTP METHOD ATTRIBUTES

| Attribute      | Purpose             |
|---------------|--------------------|
| [HttpGet]     | Fetch data         |
| [HttpPost]    | Create data        |
| [HttpPut]     | Update full data   |
| [HttpPatch]   | Partial update     |
| [HttpDelete]  | Delete data        |

**Example :**
```cs
[HttpGet]
public IActionResult Task<List<string>> GetAll()
```


### API Controllers

**Definition :** Controller that handles API requests


**Example :**
```cs
[ApiController]
[Route("api/[controller]")]
public class EmployeeController : ControllerBase
{
}
```


**Key Points**
- [ApiController] → Enables API features
- ControllerBase → No UI, only data

**Full Example:**
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

    [HttpPost]
    public IActionResult Create(Employee emp)
    {
        if (!ModelState.IsValid)
            return BadRequest();

        return Ok(emp);
    }
}
```
