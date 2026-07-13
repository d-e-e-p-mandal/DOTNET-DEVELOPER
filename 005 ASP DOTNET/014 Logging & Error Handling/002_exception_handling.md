# 🔹 Exception Handling in ASP.NET Core

---

# What is Exception?

Exception means:
- Runtime error
- Unexpected error

during application execution.

---

# Examples

- Divide by zero
- Database connection failure
- Null reference
- File not found

---

# Example

```cs
int x = 10 / 0;
```

Produces:

```text
DivideByZeroException
```

---

# What is Exception Handling?

Exception handling means:
- Catching errors
- Preventing application crash
- Returning proper response

---

# Simple Meaning

```text
Exception Handling
    ↓
Handling Runtime Errors Safely
```

---

# Why Exception Handling Important?

Used for:
- Prevent app crash
- Show user-friendly errors
- Log errors
- Improve security

---

# Exception Handling Types

- try-catch
- Global Exception Handling
- Exception Middleware

---

# 1. try-catch

---

# What is try-catch?

Used to catch exceptions manually.

---

# Syntax

```cs
try
{

}
catch(Exception ex)
{

}
```

---

# Flow

```text
Try Code
   ↓
Error Occurs ?
 ↓          ↓
NO          YES
 ↓            ↓
Continue    Catch Block Runs
```

---

# Example

```cs
try
{
    int x = 10 / 0;
}
catch(Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

---

# Output

```text
Attempted to divide by zero.
```

---

# Explanation

---

# try Block

```cs
try
{
    
}
```

Code that may produce error.

---

# catch Block

```cs
catch(Exception ex)
{
    
}
```

Catches exception.

---

# Exception ex

Contains:
- Error message
- Stack trace
- Error details

---

# ex.Message

```cs
ex.Message
```

Returns:
- Error message

---

# Example

```cs
Console.WriteLine(ex.Message);
```

---

# Controller Example

```cs
[HttpGet]
public IActionResult Get()
{
    try
    {
        int x = 10 / 0;

        return Ok(x);
    }
    catch(Exception ex)
    {
        return BadRequest(ex.Message);
    }
}
```

---

# Result

```text
400 Bad Request
```

with error message.

---

# Multiple catch Blocks

```cs
try
{

}
catch(DivideByZeroException ex)
{

}
catch(Exception ex)
{

}
```

---

# finally Block

```cs
finally
{
    Console.WriteLine("Always Runs");
}
```

---

# Purpose

Runs always:
- Error or no error

---

# Example

```cs
try
{
    int x = 10 / 2;
}
catch(Exception ex)
{
    
}
finally
{
    Console.WriteLine("Finished");
}
```

---

# Output

```text
Finished
```

---

# try-catch Advantages

- Simple
- Easy error handling

---

# try-catch Disadvantages

- Repeated code
- Hard to manage globally

---

# Simple Meaning

```text
try-catch
    ↓
Local Error Handling
```

---

# 2. Global Exception Handling

---

# What is Global Exception Handling?

Handles errors for entire application.

---

# Purpose

Used for:
- Centralized error handling
- Common error response
- Cleaner code

---

# Problem Without Global Handling

Every controller needs:

```cs
try-catch
```

---

# Example

```cs
public IActionResult Get()
{
    try
    {

    }
    catch(Exception ex)
    {

    }
}
```

Repeated everywhere.

---

# Solution

```text
Global Exception Handling
```

---

# Global Error Flow

```text
Request
   ↓
Controller Error
   ↓
Global Exception Handler
   ↓
Return Common Response
```

---

# ASP.NET Built-in Global Handler

## Program.cs

```cs
app.UseExceptionHandler("/Error");
```

---

# Purpose

Handles unhandled exceptions globally.

---

# Example Controller

```cs
[Route("Error")]
public IActionResult Error()
{
    return Problem(
        "Something Went Wrong");
}
```

---

# Result

```text
500 Internal Server Error
```

---

# Benefits

- Centralized handling
- Cleaner controllers
- Common error format

---

# Production Usage

Mostly:
- Global handling preferred

---

# Simple Meaning

```text
Global Exception Handling
    ↓
One Place Handles All Errors
```

---

# 3. Exception Middleware

---

# What is Exception Middleware?

Custom middleware used to handle exceptions globally.

---

# Purpose

Used for:
- Global error handling
- Logging errors
- Custom error response

---

# Why Middleware?

Middleware can catch:
- All application errors

---

# Exception Middleware Flow

```text
Request
   ↓
Middleware
   ↓
Controller Error
   ↓
Middleware Catches Error
   ↓
Return Error Response
```

---

# Create Middleware Folder

```text
Project
│
├── Middleware/
│      └── ExceptionMiddleware.cs
```

---

# Exception Middleware Example

```cs
public class ExceptionMiddleware
{
    private readonly RequestDelegate
        _next;

    public ExceptionMiddleware(
        RequestDelegate next)
    {
        _next = next;
    }

    public async Task Invoke(
        HttpContext context)
    {
        try
        {
            await _next(context);
        }
        catch(Exception ex)
        {
            context.Response.StatusCode = 500;

            await context.Response
                .WriteAsync(
                    "Internal Server Error");
        }
    }
}
```

---

# Explanation

---

# _next(context)

```cs
await _next(context);
```

Runs next middleware/controller.

---

# try Block

Runs application request.

---

# catch Block

Catches any exception.

---

# Response.StatusCode

```cs
context.Response.StatusCode = 500;
```

Returns:
- 500 Internal Server Error

---

# WriteAsync()

```cs
WriteAsync()
```

Writes response message.

---

# Register Middleware

## Program.cs

```cs
app.UseMiddleware<ExceptionMiddleware>();
```

---

# IMPORTANT

Middleware should be near top of pipeline.

---

# Example

```cs
app.UseMiddleware<ExceptionMiddleware>();

app.UseAuthentication();

app.UseAuthorization();
```

---

# Why?

To catch all errors.

---

# Complete Flow

```text
Request
   ↓
Exception Middleware
   ↓
Controller Executes
   ↓
Error Occurs
   ↓
Middleware Catches Error
   ↓
Return Error Response
```

---

# Example Error Response

```json
{
  "message":
  "Internal Server Error"
}
```

---

# Better JSON Response

```cs
await context.Response.WriteAsJsonAsync(
    new
    {
        StatusCode = 500,
        Message = ex.Message
    });
```

---

# Output

```json
{
  "statusCode": 500,
  "message":
  "Attempted to divide by zero."
}
```

---

# Logging Errors in Middleware

```cs
Console.WriteLine(ex.Message);
```

---

# Industry Usage

Mostly middleware used with:
- Serilog
- ILogger

---

# Production Best Practice

Do NOT expose:
- Real exception details

to users.

---

# Instead Return

```text
Something Went Wrong
```

---

# Exception Types

| Exception | Meaning |
|---|---|
| DivideByZeroException | Divide by zero |
| NullReferenceException | Null object |
| SqlException | Database error |
| FileNotFoundException | Missing file |

---

# Status Codes

| Code | Meaning |
|---|---|
| 400 | Bad Request |
| 401 | Unauthorized |
| 403 | Forbidden |
| 404 | Not Found |
| 500 | Internal Server Error |

---

# try-catch vs Global vs Middleware

| Feature | try-catch | Global | Middleware |
|---|---|
| Scope | Local | Entire App | Entire App |
| Reusable | No | Yes | Yes |
| Logging | Manual | Easy | Best |
| Industry Use | Small logic | Common | Most common |

---

# Exception Handling Pipeline

```text
Client Request
        ↓
Middleware
        ↓
Controller
        ↓
Exception Occurs
        ↓
Middleware/Global Handler
        ↓
Error Response
```

---

# Real-Life Analogy

| ASP.NET Core | Real Life |
|---|---|
| try-catch | Local repair |
| Global Exception Handler | Main complaint desk |
| Exception Middleware | Emergency control room |
| Exception | System failure |
| Error Response | Warning message |

---

# SIMPLE UNDERSTANDING

```text
try-catch
    ↓
Handle Local Errors

Global Exception Handling
    ↓
Handle Application Errors

Exception Middleware
    ↓
Central Error Control System
```