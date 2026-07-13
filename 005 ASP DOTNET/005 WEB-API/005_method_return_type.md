[Return Type]() [IActionResult]()
- **For web Use asyn function using Task and IActionResult. Describe at bellow.**

# Return Type in ASP DOTNET:


-----------------------------------
## Simple Return Type Without Async:

### DIRECT TYPE (T) → ONLY DATA
```cs
public Employee Get()
{
    return new Employee();
}
```
- Returns data only
- Auto → 200 OK
- No error/status control


## COLLECTION TYPES

### List<T>
```cs
public List<Employee> Get()
{
    return _context.Employees.ToList();
}
```
- Concrete collection

### IEnumerable<T>
```CS
public IEnumerable<Employee> Get()
{
    return _context.Employees.ToList();
}
```
- In-memory collection


# IQueryable<T>

```cs
public IQueryable<Employee> Get()
{
    return _context.Employees;
}
```
- Employee - Model or DTOs 
- DB query (lazy execution)
- Used to return linq query.


### ICollection<T> 
```cs
public ICollection<Employee> Get()
{
    return new List<Employee>();
}
```
- Supports add/remove

### 3. IActionResult (CORE/Best Use)
```cs
public IActionResult Get()
{
    return Ok("Hello");
}
```
- ✔ Full control
- ✔ Any status code

### ActionResult<T>
```cs
public ActionResult<Employee> Get(int id)
{
    var emp = _context.Employees.Find(id);
    if (emp == null)
        return NotFound();
    return emp;
}
```
- ✔ Strongly typed

--------------------------------------------
# Web : ASYNC RETURN TYPES : Task<T>
- Use keyword `async`.
- Bind each return type with `Task`. Task is used to assign Thread.

**Example List:**

```cs
public async Task<List<Employee>> Get()
{
    return await _context.Employees.ToListAsync();
}
```


### Task<IActionResult> 
```cs
public async Task<IActionResult> Get()
{
    return Ok(await _context.Employees.ToListAsync());
}
```
- Used In Controller (Best Use)

### Task<ActionResult<T>> 
```cs
public async Task<ActionResult<List<Employee>>> Get()
{
    var data = await _context.Employees.ToListAsync();
    if (!data.Any())
        return NotFound();
    return data;
}
```

## STREAMING TYPES

### IAsyncEnumerable<T>
```cs
public async IAsyncEnumerable<Employee> Get()
{
    await foreach (var emp in _context.Employees.AsAsyncEnumerable())
    {
        yield return emp;
    }
}
```
- Large data streaming

**MIXED TYPE RETURNS :**

### Combination
```cs
public ActionResult<IEnumerable<Employee>> Get()
{
    return _context.Employees.ToList();
}
```

### EDGE CASES / ADVANCED


### ValueTask<T>
```cs
public async ValueTask<Employee> Get()
{
    return new Employee();
}
```
- Rare optimization


### void / Task

public void Get() { }     // not recommended
public Task Get() { }     // avoid


EXAMPLE :
```cs
[HttpGet]
public async Task<ActionResult<IEnumerable<Employee>>> GetEmployees()
{
    IQueryable<Employee> query = _context.Employees;
    query = query.Where(e => e.Salary > 1000);
    var data = await query.ToListAsync();
    if (!data.Any())
        return NotFound();
    return data;
}
```

-------------------------------------------------------------
# IActionResult:

## Internal Code of IActionResult

**It’s just an interface :**

**Actual concept :**
```cs
public interface IActionResult
{
    Task ExecuteResultAsync(ActionContext context);
}
```
```cs
public async Task ExecuteResultAsync(ActionContext context)
{
    var response = context.HttpContext.Response;

    response.StatusCode = 200;

    await response.WriteAsJsonAsync("Hello"); // value : Hellow
}
```

### 2. Example Internal Class (OkObjectResult)
```cs
public class OkObjectResult : ObjectResult
{
    public OkObjectResult(object value) : base(value)
    {
        StatusCode = 200;
    }
}
```

### 3. Core Internal Logic (ObjectResult)
```cs
public class ObjectResult : IActionResult
{
    public object Value { get; set; }
    public int? StatusCode { get; set; }
    public ObjectResult(object value)
    {
        Value = value;
    }
    public async Task ExecuteResultAsync(ActionContext context)
    {
        var response = context.HttpContext.Response;
        response.StatusCode = StatusCode ?? 200;
        // Convert object → JSON
        await response.WriteAsJsonAsync(Value);
    }
}
```
- THIS is the real engine :
- Sets status code :
- Serializes data :
- Sends response :


### 4. Internal Code of ActionResult

- It’s just a wrapper class :
```cs
public abstract class ActionResult : IActionResult
{
    public virtual Task ExecuteResultAsync(ActionContext context)
    {
        throw new NotImplementedException();
    }
}
```
- Most real results (Ok, NotFound, etc.) inherit from this or similar base classes.


### 5. Internal Code of ActionResult<T> (Important)
```cs
public class ActionResult<T> : IActionResult
{
    private readonly IActionResult _result;
    private readonly T _value;
    public ActionResult(T value)
    {
        _value = value;
    }
    public ActionResult(IActionResult result)
    {
        _result = result;
    }
    public async Task ExecuteResultAsync(ActionContext context)
    {
        if (_result != null)
        {
            await _result.ExecuteResultAsync(context);
        }
        else
        {
            var objectResult = new ObjectResult(_value);
            await objectResult.ExecuteResultAsync(context);
        }
    }
}
```

⚔️ Internal Difference (Code Level)

### IActionResult
```cs
return Ok();  // Already a result object
```
**Framework just calls: :**
```cs
ExecuteResultAsync()
```

### ActionResult
- Same behavior — no extra logic :

### ActionResult<T>
```cs
return "Hello";
```
**Internally becomes: :**
```cs
new ObjectResult("Hello")
```
**Because of: :**
```cs
if (_result != null)
   // use it
else
    //wrap value
```
