# Built-in Middleware in ASP.NET Core

---

# What is Built-in Middleware?

Built-in Middleware are pre-made middleware components provided by ASP.NET Core.

Used for:
- Routing
- Authentication
- Security
- Static files
- Sessions
- CORS
- Logging

---

# Middleware Flow

```text
Request
   ↓
Middleware 1
   ↓
Middleware 2
   ↓
Middleware 3
   ↓
Controller
   ↓
Response
```

---

# Middleware Added in Program.cs

```cs
var app = builder.Build();

app.UseHttpsRedirection();

app.UseStaticFiles();

app.UseRouting();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();

app.Run();
```

---

# 1. UseRouting()

```cs
app.UseRouting();
```

---

# Purpose

Enables routing system.

Matches URL with controller/action.

---

# Flow

```text
URL
 ↓
Routing Middleware
 ↓
Find Matching Endpoint
```

---

# Example

```text
/api/employee
```

Routing finds:

```text
EmployeeController
```

---

# IMPORTANT

Must come before:

```cs
UseAuthorization()
```

---

# Simple Meaning

```text
UseRouting = Route Finder
```

---

# 2. UseAuthentication()

```cs
app.UseAuthentication();
```

---

# Purpose

Checks user identity.

Used for:
- JWT Token
- Login
- Cookies
- Identity

---

# Flow

```text
Request
 ↓
Check User Login
 ↓
User Authenticated
```

---

# Example

```text
Authorization: Bearer TOKEN
```

Middleware validates token.

---

# If Authentication Fails

```text
401 Unauthorized
```

returned.

---

# IMPORTANT

Must come before:

```cs
UseAuthorization()
```

---

# Simple Meaning

```text
UseAuthentication = Identity Checker
```

---

# 3. UseAuthorization()

```cs
app.UseAuthorization();
```

---

# Purpose

Checks permissions and roles.

---

# Example

```cs
[Authorize(Roles = "Admin")]
```

Middleware checks:
- Is user Admin?

---

# If Authorization Fails

```text
403 Forbidden
```

returned.

---

# Flow

```text
Authenticated User
        ↓
Check Permissions
        ↓
Allow or Deny
```

---

# Simple Meaning

```text
UseAuthorization = Permission Checker
```

---

# 4. UseStaticFiles()

```cs
app.UseStaticFiles();
```

---

# Purpose

Serves static files.

---

# Static Files Examples

- CSS
- JavaScript
- Images
- PDFs

---

# Default Folder

```text
wwwroot
```

---

# Example Structure

```text
wwwroot/
│
├── css/
├── js/
├── images/
```

---

# Example URL

```text
https://localhost:5001/images/logo.png
```

---

# Without UseStaticFiles()

Static files cannot open.

---

# Simple Meaning

```text
UseStaticFiles = Public File Access
```

---

# 5. UseHttpsRedirection()

```cs
app.UseHttpsRedirection();
```

---

# Purpose

Redirects:
- HTTP → HTTPS

---

# Example

---

# User Opens

```text
http://localhost:5000
```

---

# Middleware Redirects To

```text
https://localhost:5001
```

---

# Purpose

Improves security.

---

# Simple Meaning

```text
UseHttpsRedirection = Secure Redirect
```

---

# 6. UseCors()

```cs
app.UseCors();
```

---

# Purpose

Allows frontend applications to access API.

---

# Example Frontend

- React
- Angular
- Vue

---

# Example

```cs
app.UseCors(policy =>
    policy.AllowAnyOrigin()
          .AllowAnyMethod()
          .AllowAnyHeader());
```

---

# Without CORS

Browser blocks API requests.

---

# Simple Meaning

```text
UseCors = Frontend Access Permission
```

---

# 7. UseExceptionHandler()

```cs
app.UseExceptionHandler();
```

---

# Purpose

Handles application errors globally.

---

# Example

```cs
app.UseExceptionHandler("/Error");
```

---

# Purpose

Shows custom error page.

---

# Simple Meaning

```text
UseExceptionHandler = Global Error Handler
```

---

# 8. UseDeveloperExceptionPage()

```cs
app.UseDeveloperExceptionPage();
```

---

# Purpose

Shows detailed errors during development.

---

# Used In

```cs
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
```

---

# Features

- Stack trace
- Error details
- Debugging info

---

# Simple Meaning

```text
Developer Exception Page = Debug Error Screen
```

---

# 9. UseSwagger()

```cs
app.UseSwagger();
```

---

# Purpose

Generates Swagger JSON document.

---

# Used For

- API documentation
- API testing

---

# Simple Meaning

```text
UseSwagger = API Documentation Generator
```

---

# 10. UseSwaggerUI()

```cs
app.UseSwaggerUI();
```

---

# Purpose

Opens Swagger UI page.

---

# URL

```text
/swagger
```

---

# Features

- Test APIs
- View endpoints
- Send requests

---

# Simple Meaning

```text
UseSwaggerUI = API Testing Screen
```

---

# 11. UseSession()

```cs
app.UseSession();
```

---

# Purpose

Enables session management.

---

# Used For

- Store user data
- Shopping cart
- Login session

---

# Example

```cs
HttpContext.Session.SetString("Name", "Deep");
```

---

# Simple Meaning

```text
UseSession = Temporary User Storage
```

---

# 12. UseCookiePolicy()

```cs
app.UseCookiePolicy();
```

---

# Purpose

Controls cookie settings.

---

# Used For

- Cookie consent
- Cookie security

---

# Simple Meaning

```text
UseCookiePolicy = Cookie Rules Manager
```

---

# 13. UseResponseCompression()

```cs
app.UseResponseCompression();
```

---

# Purpose

Compresses API responses.

---

# Benefits

- Faster response
- Less bandwidth usage

---

# Simple Meaning

```text
UseResponseCompression = Response Size Reducer
```

---

# 14. UseHsts()

```cs
app.UseHsts();
```

---

# Purpose

Forces browser to always use HTTPS.

---

# Used In

Production environment.

---

# Simple Meaning

```text
UseHsts = HTTPS Enforcer
```

---

# 15. UseWebSockets()

```cs
app.UseWebSockets();
```

---

# Purpose

Enables WebSocket communication.

---

# Used For

- Real-time apps
- SignalR
- Chat systems

---

# Simple Meaning

```text
UseWebSockets = Real-Time Communication Support
```

---

# 16. UseStatusCodePages()

```cs
app.UseStatusCodePages();
```

---

# Purpose

Handles status code responses.

---

# Example

- 404 Page
- 500 Error

---

# Simple Meaning

```text
UseStatusCodePages = Status Error Handler
```

---

# 17. UseEndpoints()

```cs
app.UseEndpoints();
```

---

# Purpose

Maps endpoints.

---

# Example

```cs
app.UseEndpoints(endpoints =>
{
    endpoints.MapControllers();
});
```

---

# NOTE

Mostly old architecture (.NET 5).

New architecture uses:

```cs
app.MapControllers();
```

---

# Simple Meaning

```text
UseEndpoints = Endpoint Mapper
```

---

# 18. MapControllers()

```cs
app.MapControllers();
```

---

# Purpose

Maps controller routes.

---

# Used For

- Web APIs
- MVC Controllers

---

# Simple Meaning

```text
MapControllers = Connect Routes to Controllers
```

---

# Complete Middleware Flow

```text
Client Request
        ↓
UseHttpsRedirection
        ↓
UseStaticFiles
        ↓
UseRouting
        ↓
UseAuthentication
        ↓
UseAuthorization
        ↓
MapControllers
        ↓
Controller Executes
        ↓
Response Returned
```

---

# IMPORTANT

Middleware Order Matters.

---

# Correct Order Example

```cs
app.UseRouting();

app.UseAuthentication();

app.UseAuthorization();

app.MapControllers();
```

---

# Why?

Because:
- Routing finds endpoint first
- Authentication checks identity
- Authorization checks permissions

---

# Middleware Categories

| Middleware | Category |
|---|---|
| UseRouting | Routing |
| UseAuthentication | Security |
| UseAuthorization | Security |
| UseStaticFiles | Static Files |
| UseCors | Cross-Origin |
| UseSwagger | API Documentation |
| UseSession | State Management |
| UseResponseCompression | Performance |
| UseExceptionHandler | Error Handling |

---

# Real-Life Analogy

| Middleware | Real Life |
|---|---|
| UseRouting | GPS |
| UseAuthentication | ID Check |
| UseAuthorization | Permission Check |
| UseStaticFiles | Public File Counter |
| UseHttpsRedirection | Security Gate |
| UseCors | Visitor Permission |
| UseSwaggerUI | API Manual |