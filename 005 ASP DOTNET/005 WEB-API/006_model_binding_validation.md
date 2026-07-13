[Model Binding : Form]() [Internal working]()

# MODEL BINDING & VALIDATION

Definition : Convert incoming request data → C# object automatically

Example : Client sends JSON:
```json
{
  "name": "Deep",
  "salary": 50000
}
```

Controller receives:
```cs
[HttpPost]
public IActionResult Create(Employee emp)
{
    return Ok(emp);
}
```
Automatically converted to: `Employee emp`

Sources of Data : Model binding can read from:
* Body (JSON)
* Route
* Query string
* Form data

⸻

Example (Route)
```cs
[HttpGet("{id}")]
public IActionResult Get(int id)
```
URL: /api/employee/5
id = 5


## MODEL BINDING ATTRIBUTES (From*)

Used to tell ASP.NET: “Data is coming from where?”

### [FromBody]

Meaning : Read data from request body (JSON)

```cs
[HttpPost]
public IActionResult Create([FromBody] Employee emp)
{
    return Ok(emp);
}
```

Request :
```json
{
  "name": "Deep",
  "salary": 50000
}
```

Notes :

* Used in POST / PUT
* Only one FromBody allowed
* Uses JSON deserialization

### [FromQuery]
Meaning : Read from query string

Example :
```cs
[HttpGet]
public IActionResult Get([FromQuery] int id)
{
    return Ok(id);
}
```
URL : /api/employee?id=5

Notes :
* Used in GET
* Good for filters, pagination

### [FromQuery(Name = "...")]

Meaning : Rename query parameter

Example : 
```cs
[HttpGet]
public IActionResult Get([FromQuery(Name = "emp_id")] int id)
{
    return Ok(id);
}
```
URL : /api/employee?emp_id=5

### [FromRoute]

Meaning : Read from URL path

Example :
```cs
[HttpGet("{id}")]
public IActionResult Get([FromRoute] int id)
{
    return Ok(id);
}
```
URL  : /api/employee/5

Notes :
* Used for resource identification
* Matches route parameter

### [FromRoute(Name = "...")]
```cs
[HttpGet("{emp_id}")]
public IActionResult Get([FromRoute(Name = "emp_id")] int id)
{
    return Ok(id);
}
```


### [FromForm]

Meaning : Read from form-data

Example :
```cs
[HttpPost]
public IActionResult Upload([FromForm] string name)
{
    return Ok(name);
}
```
Used for :
* File upload
* HTML forms


### [FromHeader]

Meaning : Read from request headers

Example
```cs
[HttpGet]
public IActionResult Get([FromHeader] string token)
{
    return Ok(token);
}
```
Header : token: abc123

### [FromServices]

Meaning : Inject service from Dependency Injection

Example
```cs
[HttpGet]
public IActionResult Get([FromServices] ILogger logger)
{
    return Ok("Service injected");
}
```
Notes :

* Rarely used in parameters
* Usually use constructor injection


----------
```
Attribute	Source
FromBody	JSON body
FromQuery	Query string
FromRoute	URL path
FromForm	Form-data
FromHeader	Headers
FromServices	DI container
```

- AUTO BEHAVIOR (VERY IMPORTANT)
- With [ApiController]:

Simple types (int, string) → FromQuery  
Complex types (class) → FromBody  


FULL EXAMPLE (ALL TOGETHER):
```cs
[HttpPost("{id}")]
public IActionResult Test(
    [FromRoute] int id,            // URL
    [FromQuery] string name,       // query
    [FromHeader] string token,     // header
    [FromBody] Employee emp        // body
)
{
    return Ok(new { id, name, token, emp });
}
```



-----------------------------------------------
----

### INTERNAL CODE FLOW

Step 1: Read Request Body

ASP.NET reads raw request body:
```cs
var bodyStream = httpContext.Request.Body;
using var reader = new StreamReader(bodyStream);
string json = await reader.ReadToEndAsync();
```
Now: json = "{ \"name\": \"Deep\", \"salary\": 50000 }"

Step 2: Deserialize JSON → Object

Uses built-in JSON serializer:
```cs
var employee = JsonSerializer.Deserialize<Employee>(json);
```

🔄Internally this happens:
```cs
// pseudo internal logic
Employee emp = new Employee();
emp.Name = json["name"];   // map value
emp.Salary = json["salary"];
```
Step 3: Property Matching

**ASP.NET uses reflection to match properties:**
```cs
foreach (var property in typeof(Employee).GetProperties())
{
    var value = jsonData[property.Name.ToLower()];
    property.SetValue(emp, Convert(value));
}
```

**Step 4: ModelState Creation**

ModelState["Name"] = "Deep";
ModelState["Salary"] = 50000;

Also tracks errors

**Step 5: Validation (Annotations)**
```cs
if (emp.Name == null)
{
    ModelState.AddError("Name", "Required");
}
```

**Step 6: Pass to Controller**
```cs
public IActionResult Create(Employee emp)
```
Now:
```cs
emp.Name = "Deep";
emp.Salary = 50000;
```

REAL ASP.NET CORE CLASSES (ACTUAL INTERNAL) :
ASP.NET actually uses:
- * ModelBinder
- * BodyModelBinder
- * SystemTextJsonInputFormatter

**Actual internal call (simplified)**
```cs
var formatter = new SystemTextJsonInputFormatter(...);
var result = await formatter.ReadRequestBodyAsync(context);
var model = result.Model;
```

**Core Line (REAL ENGINE)**
```cs
JsonSerializer.Deserialize<T>(json, options);
```

FULL INTERNAL FLOW :
```
HTTP Request
   ↓
Read Body Stream
   ↓
Convert Stream → String (JSON)
   ↓
JsonSerializer.Deserialize<T>()
   ↓
Reflection → Map properties
   ↓
Create Object (Employee)
   ↓
Validate → ModelState
   ↓
Pass to Controller
```

SIMPLE UNDERSTANDING : ASP.NET internally does:
```cs
var json = ReadBody();
var obj = JsonSerializer.Deserialize<T>(json);
return obj;
```

-------------------------------