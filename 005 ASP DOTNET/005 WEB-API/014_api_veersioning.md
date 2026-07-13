# API Versioning in ASP.NET Core

---

# What is API Versioning?

API Versioning is a technique used to maintain multiple versions of APIs.

---

# Purpose

Used for:
- Updating APIs safely
- Supporting old clients
- Adding new features
- Preventing breaking changes

---

# Problem Without Versioning

Suppose old API:

```text
/api/employee
```

Frontend applications already use it.

Now API changes:
- Response structure changes
- Parameters change

Old applications may break.

---

# Solution

Create multiple versions.

Example:

```text
/api/v1/employee
/api/v2/employee
```

---

# Simple Meaning

```text
API Versioning = Multiple Versions of Same API
```

---

# Why API Versioning Important?

Used to:
- Maintain backward compatibility
- Improve APIs safely
- Support old mobile/web apps

---

# Real Example

| Version | Purpose |
|---|---|
| v1 | Old API |
| v2 | Improved API |
| v3 | Latest API |

---

# API Versioning Package

Install package:

```bash
dotnet add package Microsoft.AspNetCore.Mvc.Versioning
```

---

# Program.cs Setup

```cs
var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();

builder.Services.AddApiVersioning(options =>
{
    // Default Version
    options.DefaultApiVersion =
        new ApiVersion(1, 0);

    // Use Default Version
    options.AssumeDefaultVersionWhenUnspecified = true;

    // Report Supported Versions
    options.ReportApiVersions = true;
});

var app = builder.Build();

app.MapControllers();

app.Run();
```

---

# Explanation

---

# AddApiVersioning()

```cs
builder.Services.AddApiVersioning()
```

## Purpose

Enables API versioning support.

---

# DefaultApiVersion

```cs
options.DefaultApiVersion =
    new ApiVersion(1, 0);
```

## Meaning

Default version becomes:

```text
v1.0
```

---

# AssumeDefaultVersionWhenUnspecified

```cs
options.AssumeDefaultVersionWhenUnspecified = true;
```

## Meaning

If client does not provide version:

```text
Automatically use default version
```

---

# ReportApiVersions

```cs
options.ReportApiVersions = true;
```

## Purpose

Returns supported versions in response headers.

---

# Versioning Methods

ASP.NET Core supports multiple versioning styles.

---

# 1. URL Versioning (Most Common)

---

# Example URL

```text
/api/v1/employee
/api/v2/employee
```

---

# Controller Example

## Version 1 Controller

```cs
using Microsoft.AspNetCore.Mvc;

[ApiVersion("1.0")]

[Route("api/v{version:apiVersion}/[controller]")]
[ApiController]
public class EmployeeController : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok("Employee API Version 1");
    }
}
```

---

# URL

```text
/api/v1/employee
```

---

# Output

```text
Employee API Version 1
```

---

# Version 2 Controller

```cs
using Microsoft.AspNetCore.Mvc;

[ApiVersion("2.0")]

[Route("api/v{version:apiVersion}/[controller]")]
[ApiController]
public class EmployeeV2Controller : ControllerBase
{
    [HttpGet]
    public IActionResult Get()
    {
        return Ok("Employee API Version 2");
    }
}
```

---

# URL

```text
/api/v2/employeev2
```

---

# Output

```text
Employee API Version 2
```

---

# Route Explanation

```cs
[Route("api/v{version:apiVersion}/[controller]")]
```

---

# Meaning

| Part | Meaning |
|---|---|
| api | Base route |
| v{version} | API version |
| [controller] | Controller name |

---

# 2. Query String Versioning

---

# URL Example

```text
/api/employee?api-version=1.0
```

---

# Setup

```cs
options.ApiVersionReader =
    new QueryStringApiVersionReader("api-version");
```

---

# Purpose

Reads version from query string.

---

# 3. Header Versioning

---

# Request Header

```text
api-version: 1.0
```

---

# Setup

```cs
options.ApiVersionReader =
    new HeaderApiVersionReader("api-version");
```

---

# Purpose

Reads version from request header.

---

# 4. Media Type Versioning

---

# Example Header

```text
Accept: application/json;v=1.0
```

---

# Purpose

Reads version from media type.

---

# Commonly Used Versioning Style

| Versioning Type | Industry Usage |
|---|---|
| URL Versioning | Most Common |
| Query String | Sometimes |
| Header Versioning | Enterprise APIs |
| Media Type | Rare |

---

# Version Neutral API

Some APIs work for all versions.

---

# Example

```cs
[ApiVersionNeutral]
```

---

# Purpose

API works for:
- v1
- v2
- v3

---

# Multiple Versions in Same Controller

```cs
[ApiVersion("1.0")]
[ApiVersion("2.0")]
```

---

# Map Action to Specific Version

```cs
[MapToApiVersion("2.0")]
```

---

# Example

```cs
[HttpGet]
[MapToApiVersion("2.0")]
public IActionResult GetV2()
{
    return Ok("Version 2");
}
```

---

# Swagger Integration with API Versioning

Swagger can show:
- v1 APIs
- v2 APIs

Separately.

---

# Common API Versioning Flow

```text
Client Request
      ↓
Version Read
      ↓
Correct Controller Selected
      ↓
Action Method Executed
      ↓
Response Returned
```

---

# Benefits of API Versioning

- Backward compatibility
- Safer API updates
- Better maintainability
- Supports old clients

---

# Problems Without API Versioning

- Frontend breaks
- Mobile apps stop working
- Old clients incompatible

---

# Best Practices

- Use URL versioning
- Never break old APIs
- Keep old versions stable
- Deprecate old versions slowly

---

# API Versioning Example Structure

```text
/api/v1/employee
/api/v2/employee
/api/v3/employee
```

---

# Real-Life Analogy

| API Versioning | Real Life |
|---|---|
| v1 | Old phone model |
| v2 | Improved phone model |
| v3 | Latest phone model |
| Old APIs still work | Old phones still usable |

---

# Complete API Versioning Flow

```text
Client Sends Request
        ↓
Version Identified
        ↓
Correct API Version Selected
        ↓
Controller Executes
        ↓
Response Returned
```