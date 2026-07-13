Type Of :
[Method]() [Constructor]() [Constructor + Method]()

--------
### Using Mehtod
```cs
public class ApiResponse<T>
{
    public bool Success { get; set; }
    public string Message { get; set; }
    public T Data { get; set; }
    public object Errors { get; set; }
}
```

```cs
using Microsoft.AspNetCore.Mvc;

public static class ResponseHelper
{
    public static IActionResult Success<T>(T data, string message = "Success")
    {
        return new OkObjectResult(new ApiResponse<T>
        {
            Success = true,
            Message = message,
            Data = data,
            Errors = null
        });
    }

    public static IActionResult BadRequest(object errors, string message = "Invalid Request")
    {
        return new BadRequestObjectResult(new ApiResponse<object>
        {
            Success = false,
            Message = message,
            Data = null,
            Errors = errors
        });
    }

    public static IActionResult NotFound(string message = "Not Found")
    {
        return new NotFoundObjectResult(new ApiResponse<object>
        {
            Success = false,
            Message = message,
            Data = null,
            Errors = null
        });
    }

    public static IActionResult ServerError(string message = "Server Error")
    {
        return new ObjectResult(new ApiResponse<object>
        {
            Success = false,
            Message = message,
            Data = null,
            Errors = null
        })
        {
            StatusCode = 500
        };
    }
}
```

Use Case :
```cs
[HttpGet]
public async Task<IActionResult> GetEmployees()
{
    try
    {
        var data = await _context.Employees.ToListAsync();

        return ResponseHelper.Success(data, "Employees fetched");
    }
    catch (Exception ex)
    {
        return ResponseHelper.ServerError(ex.Message);
    }
}
```

----------------

### Using Constructor :
```cs
using Microsoft.AspNetCore.Mvc;

public class ApiResponse<T>
{
    public bool Success { get; set; }
    public string Message { get; set; }
    public T Data { get; set; }
    public object Errors { get; set; }

    // Success Constructor
    public ApiResponse(T data, string message = "Success")
    {
        Success = true;
        Message = message;
        Data = data;
        Errors = null;
    }

    // Error Constructor
    public ApiResponse(string message, object errors = null)
    {
        Success = false;
        Message = message;
        Data = default;
        Errors = errors;
    }

    // Convert to IActionResult
    public IActionResult ToOkResult()
    {
        return new OkObjectResult(this);
    }

    pu
    blic IActionResult ToBadRequest()
    {
        return new BadRequestObjectResult(this);
    }

    public IActionResult ToNotFound()
    {
        return new NotFoundObjectResult(this);
    }
}

```
Calling :
```cs
[HttpGet]
public async Task<IActionResult> GetEmployees()
{
    var data = await _context.Employees.ToListAsync();

    re
    turn new ApiResponse<List<Employee>>(data, "Fetched successfully")
           .ToOkResult();
}
```

------------

### Constructor And Method Both Used: (Industry level)
```cs
public class ApiResponse<T>
{
    public bool Success { get; set; }
    public string Message { get; set; }
    public T Data { get; set; }
    public object Errors { get; set; }

    // Success Method
    public static ApiResponse<T> SuccessResponse(T data, string message = "Success")
    {
        return new ApiResponse<T>
        {
            Success = true,
            Message = message,
            Data = data,
            Errors = null
        };
    }

    // Fail Method
    public static ApiResponse<T> FailResponse(string message, object errors = null)
    {
        return new ApiResponse<T>
        {
            Success = false,
            Message = message,
            Data = default,
            Errors = errors
        };
    }
}
```

```cs
[HttpGet]
public async Task<IActionResult> GetEmployees()
{
    var data = await _context.Employees.ToListAsync();

    return Ok(ApiResponse<List<Employee>>
              .SuccessResponse(data, "Fetched successfully"));
}
````

------------