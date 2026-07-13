# 🔹 Filters in ASP.NET Core

---

# What are Filters?

Filters are components that run:
- Before action method
- After action method

Used to add:
- Logging
- Authentication
- Error handling
- Validation

---

# Simple Meaning

```text
Filters = Extra Logic Around Controller Actions
```

---

# Why Filters Used?

Used for:
- Reusable logic
- Cleaner controllers
- Centralized processing

---

# Example Uses

- Check login
- Log request
- Catch exceptions
- Modify response

---

# Filter Flow

```text
Request
   ↓
Filters
   ↓
Controller Action
   ↓
Filters
   ↓
Response
```

---

# Filter Pipeline

ASP.NET Core executes filters in pipeline order.

---

# Filter Pipeline Flow

```text
Request
   ↓
Authorization Filter
   ↓
Action Filter
   ↓
Controller Action
   ↓
Result Filter
   ↓
Response
```

---

# Exception Handling

If error occurs:

```text
Exception Filter
```

handles exception.

---

# Filter Pipeline Diagram

```text
Client Request
        ↓
Authorization Filter
        ↓
Action Filter (Before)
        ↓
Controller Action
        ↓
Action Filter (After)
        ↓
Result Filter
        ↓
Response
```

---

# Types of Filters

- Action Filters
- Authorization Filters
- Exception Filters
- Result Filters

---

# 1. Action Filters

---

# What are Action Filters?

Run:
- Before action method
- After action method

---

# Purpose

Used for:
- Logging
- Validation
- Timing
- Request tracking

---

# Action Filter Flow

```text
Before Action
      ↓
Controller Action
      ↓
After Action
```

---

# Creating Action Filter

```cs
using Microsoft.AspNetCore.Mvc.Filters;

public class MyActionFilter
    : IActionFilter
{
    public void OnActionExecuting(
        ActionExecutingContext context)
    {
        Console.WriteLine(
            "Before Action Executes");
    }

    public void OnActionExecuted(
        ActionExecutedContext context)
    {
        Console.WriteLine(
            "After Action Executes");
    }
}
```

---

# Explanation

---

# OnActionExecuting()

Runs BEFORE controller action.

---

# OnActionExecuted()

Runs AFTER controller action.

---

# Register Filter

```cs
[MyActionFilter]
public class EmployeeController
    : Controller
{

}
```

---

# Output

```text
Before Action Executes
Controller Action
After Action Executes
```

---

# Real Use Cases

- Request logging
- Performance tracking
- Validation

---

# Simple Meaning

```text
Action Filter = Before/After Action Logic
```

---

# 2. Authorization Filters

---

# What are Authorization Filters?

Check:
- Authentication
- Authorization
- Permissions

before controller action runs.

---

# Purpose

Used for:
- Login checking
- Role checking
- Access control

---

# Flow

```text
Request
   ↓
Authorization Check
   ↓
Allow or Deny
```

---

# Example

```cs
[Authorize]
public IActionResult Get()
{
    return Ok();
}
```

---

# What Happens?

Filter checks:
- Is user logged in?

---

# If User Not Logged In

```text
401 Unauthorized
```

returned.

---

# Role Example

```cs
[Authorize(Roles = "Admin")]
```

---

# Meaning

Only Admin can access.

---

# Custom Authorization Filter

```cs
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

public class MyAuthorizationFilter
    : IAuthorizationFilter
{
    public void OnAuthorization(
        AuthorizationFilterContext context)
    {
        var user =
            context.HttpContext.User;

        if (!user.Identity.IsAuthenticated)
        {
            context.Result =
                new UnauthorizedResult();
        }
    }
}
```

---

# Explanation

---

# User.Identity.IsAuthenticated

Checks:
- User logged in or not

---

# UnauthorizedResult()

Returns:

```text
401 Unauthorized
```

---

# Simple Meaning

```text
Authorization Filter = Permission Checker
```

---

# 3. Exception Filters

---

# What are Exception Filters?

Handle exceptions globally.

---

# Purpose

Used for:
- Error handling
- Custom error responses

---

# Flow

```text
Action Error
      ↓
Exception Filter
      ↓
Error Response
```

---

# Example

```cs
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Mvc.Filters;

public class MyExceptionFilter
    : IExceptionFilter
{
    public void OnException(
        ExceptionContext context)
    {
        context.Result =
            new ObjectResult(
                "Something Went Wrong")
            {
                StatusCode = 500
            };

        context.ExceptionHandled = true;
    }
}
```

---

# Explanation

---

# OnException()

Runs when exception occurs.

---

# ExceptionHandled

```cs
context.ExceptionHandled = true;
```

Means:
- Exception already handled

---

# Result

Returns:

```text
500 Internal Server Error
```

---

# Benefits

- Centralized error handling
- Cleaner controllers

---

# Simple Meaning

```text
Exception Filter = Error Handler
```

---

# 4. Result Filters

---

# What are Result Filters?

Run:
- Before response
- After response

---

# Purpose

Used for:
- Modifying response
- Logging response
- Response formatting

---

# Flow

```text
Controller Result
      ↓
Result Filter
      ↓
Response Sent
```

---

# Example

```cs
using Microsoft.AspNetCore.Mvc.Filters;

public class MyResultFilter
    : IResultFilter
{
    public void OnResultExecuting(
        ResultExecutingContext context)
    {
        Console.WriteLine(
            "Before Result");
    }

    public void OnResultExecuted(
        ResultExecutedContext context)
    {
        Console.WriteLine(
            "After Result");
    }
}
```

---

# Explanation

---

# OnResultExecuting()

Runs BEFORE response sent.

---

# OnResultExecuted()

Runs AFTER response sent.

---

# Simple Meaning

```text
Result Filter = Response Handler
```

---

# Registering Filters

---

# Controller Level

```cs
[MyActionFilter]
public class EmployeeController
    : Controller
{

}
```

---

# Action Level

```cs
[MyActionFilter]
public IActionResult Get()
{
    
}
```

---

# Global Filter

---

# Program.cs

```cs
builder.Services.AddControllers(
    options =>
{
    options.Filters.Add<
        MyActionFilter>();
});
```

---

# Purpose

Applies filter to all controllers.

---

# Filter Execution Order

```text
Authorization Filter
        ↓
Action Filter
        ↓
Controller Action
        ↓
Result Filter
```

---

# Exception Case

```text
Controller Error
        ↓
Exception Filter
```

---

# Filter Types Summary

| Filter | Purpose |
|---|---|
| Action Filter | Before/After Action |
| Authorization Filter | Security |
| Exception Filter | Error Handling |
| Result Filter | Response Handling |

---

# Filters vs Middleware

| Filters | Middleware |
|---|---|
| MVC/Web API only | Entire application |
| Runs around actions | Runs in pipeline |
| Controller-focused | Request-focused |

---

# Real-Life Analogy

| ASP.NET Core Filter | Real Life |
|---|---|
| Authorization Filter | Security Guard |
| Action Filter | Attendance Checker |
| Exception Filter | Emergency Handler |
| Result Filter | Final Quality Check |
| Filter Pipeline | Airport Security Process |

---

# COMPLETE FILTER FLOW

```text
Client Request
        ↓
Authorization Filter
        ↓
Action Filter
        ↓
Controller Action
        ↓
Result Filter
        ↓
Response
```