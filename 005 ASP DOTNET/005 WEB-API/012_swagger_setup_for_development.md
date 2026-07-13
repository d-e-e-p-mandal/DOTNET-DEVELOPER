# Swagger Setup with Development Mode in ASP.NET Core

```cs
var builder = WebApplication.CreateBuilder(args);

// Add Controllers
builder.Services.AddControllers();

// Add Endpoint Explorer
builder.Services.AddEndpointsApiExplorer();

// Add Swagger Generator
builder.Services.AddSwaggerGen();

var app = builder.Build();


// Enable Swagger Only In Development
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();

    app.UseSwaggerUI();
}


// HTTPS Redirection
app.UseHttpsRedirection();

// Authorization
app.UseAuthorization();

// Map Controllers
app.MapControllers();

// Run Application
app.Run();
```

---

# Explanation

---

# Create Builder

```cs
var builder = WebApplication.CreateBuilder(args);
```

## Purpose

Creates ASP.NET Core application builder.

Contains:
- Services
- Configuration
- Logging
- Environment

---

# AddControllers()

```cs
builder.Services.AddControllers();
```

## Purpose

Enables API Controllers.

Required for:
- Web APIs
- Controller routing

---

# AddEndpointsApiExplorer()

```cs
builder.Services.AddEndpointsApiExplorer();
```

## Purpose

Finds API endpoints automatically.

Used by Swagger.

---

# AddSwaggerGen()

```cs
builder.Services.AddSwaggerGen();
```

## Purpose

Generates Swagger/OpenAPI documentation.

---

# Build Application

```cs
var app = builder.Build();
```

## Purpose

Builds ASP.NET Core application.

---

# Development Mode Check

```cs
if (app.Environment.IsDevelopment())
```

## Purpose

Checks whether application is running in:

```text
Development Environment
```

---

# Why Used?

Swagger mostly used during development.

Usually disabled in production for security.

---

# UseSwagger()

```cs
app.UseSwagger();
```

## Purpose

Generates Swagger JSON document.

---

# UseSwaggerUI()

```cs
app.UseSwaggerUI();
```

## Purpose

Opens Swagger UI page in browser.

---

# Swagger URL

```text
https://localhost:5001/swagger
```

---

# UseHttpsRedirection()

```cs
app.UseHttpsRedirection();
```

## Purpose

Redirects:
- HTTP → HTTPS

---

# UseAuthorization()

```cs
app.UseAuthorization();
```

## Purpose

Checks authorization rules.

---

# MapControllers()

```cs
app.MapControllers();
```

## Purpose

Maps controller routes.

---

# Run()

```cs
app.Run();
```

## Purpose

Starts application.

---

# Complete Flow

```text
Application Starts
        ↓
Builder Created
        ↓
Services Registered
        ↓
Application Built
        ↓
Check Environment
        ↓
Enable Swagger
        ↓
Map Controllers
        ↓
Application Running
```

---

# Why Swagger Inside Development Mode?

```cs
if (app.Environment.IsDevelopment())
```

Benefits:
- Better security
- Production optimization
- Prevent public API docs exposure

---

# Environment Example

## Development

```text
ASPNETCORE_ENVIRONMENT=Development
```

Swagger Enabled.

---

## Production

```text
ASPNETCORE_ENVIRONMENT=Production
```

Swagger Disabled.

---

# 1. launchSettings.json (Most Common for Local Development)

## File Location

```text

Properties/launchSettings.json

```
```json
{
  "profiles": {
    "http": {
      "commandName": "Project",
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT":
        "Production"
      }
    }
  }
}
```
