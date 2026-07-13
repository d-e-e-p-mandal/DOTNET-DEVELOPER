# 🔹 Authentication in ASP.NET Core

---

# What is Authentication?

Authentication checks:

```text
Who are you?
```

---

# Purpose

Used for:
- Login verification
- User identity checking
- Secure APIs
- Secure websites

---

# Simple Meaning

```text
Authentication = User Identity Verification
```

---

# Example

```text
Username + Password
        ↓
System Checks User
        ↓
Valid User ?
```

---

# Authentication Flow

```text
User Sends Credentials
        ↓
Application Verifies User
        ↓
Authentication Success
        ↓
User Gets Access
```

---

# Authentication vs Authorization

| Authentication | Authorization |
|---|---|
| Who are you? | What can you access? |
| Login checking | Permission checking |

---

# Example

```text
Authentication:
"Are you employee?"

Authorization:
"Can you access admin panel?"
```

---

# Authentication Types

- Cookie Authentication
- JWT Authentication
- OAuth
- OpenID Connect

---

# Authentication Middleware

---

# Program.cs

```cs
app.UseAuthentication();

app.UseAuthorization();
```

---

# IMPORTANT ORDER

Authentication comes first.

---

# Why?

Because:
- First identify user
- Then check permissions

---

# 1. Cookie Authentication

---

# What is Cookie Authentication?

After login:
- Server creates cookie
- Browser stores cookie
- Cookie sent with every request

---

# Mostly Used In

- MVC Applications
- Traditional websites

---

# Cookie Authentication Flow

```text
User Login
      ↓
Server Creates Cookie
      ↓
Browser Stores Cookie
      ↓
Browser Sends Cookie
      ↓
Server Validates Cookie
```

---

# Program.cs Setup

```cs
builder.Services
    .AddAuthentication("CookieAuth")
    .AddCookie("CookieAuth", options =>
{
    options.LoginPath = "/Account/Login";
});
```

---

# Explanation

---

# AddAuthentication()

Enables authentication system.

---

# AddCookie()

Enables cookie authentication.

---

# LoginPath

```cs
options.LoginPath
```

Redirects unauthenticated users.

---

# Login Example

```cs
using Microsoft.AspNetCore.Authentication;
using Microsoft.AspNetCore.Authentication.Cookies;
using System.Security.Claims;

public async Task<IActionResult> Login()
{
    var claims = new List<Claim>
    {
        new Claim(ClaimTypes.Name, "Deep")
    };

    var identity =
        new ClaimsIdentity(
            claims,
            "CookieAuth");

    var principal =
        new ClaimsPrincipal(identity);

    await HttpContext.SignInAsync(
        "CookieAuth",
        principal);

    return Ok("Logged In");
}
```

---

# What Happens?

---

# Step 1

User logs in.

---

# Step 2

Server creates authentication cookie.

---

# Step 3

Browser stores cookie.

---

# Step 4

Cookie sent automatically with requests.

---

# Protect API

```cs
[Authorize]
public IActionResult Dashboard()
{
    return Ok();
}
```

---

# Logout

```cs
await HttpContext.SignOutAsync(
    "CookieAuth");
```

---

# Cookie Authentication Features

- Browser-based
- Session management
- Automatic cookie sending

---

# Simple Meaning

```text
Cookie Authentication
    ↓
Browser Stores Login Cookie
```

---

# 2. JWT Authentication

---

# What is JWT?

JWT = JSON Web Token

Token-based authentication system.

---

# Mostly Used In

- Web APIs
- Mobile Apps
- SPA Applications

---

# JWT Structure

```text
Header.Payload.Signature
```

---

# Example JWT

```text
ABC.DEF.XYZ
```

---

# JWT Flow

```text
User Login
      ↓
Server Creates JWT Token
      ↓
Client Stores Token
      ↓
Client Sends Token
      ↓
Server Validates Token
```

---

# Token Sent In Header

```text
Authorization: Bearer TOKEN
```

---

# Install Package

```bash
dotnet add package
Microsoft.AspNetCore.Authentication.JwtBearer
```

---

# Program.cs Setup

```cs
builder.Services
    .AddAuthentication("Bearer")
    .AddJwtBearer("Bearer", options =>
{
    options.TokenValidationParameters =
        new TokenValidationParameters
        {
            ValidateIssuer = false,
            ValidateAudience = false,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true
        };
});
```

---

# Explanation

---

# AddJwtBearer()

Enables JWT authentication.

---

# ValidateLifetime

Checks token expiry.

---

# ValidateIssuerSigningKey

Checks token signature.

---

# Generate JWT Token

```cs
var tokenHandler =
    new JwtSecurityTokenHandler();
```

---

# Secure API

```cs
[Authorize]
[HttpGet]
public IActionResult Get()
{
    return Ok("Secure API");
}
```

---

# Without Token

```text
401 Unauthorized
```

---

# With Valid Token

```text
200 OK
```

---

# JWT Advantages

- Stateless
- Fast
- Good for APIs
- Mobile-friendly

---

# JWT Disadvantages

- Token management needed
- Token expiration handling

---

# Cookie vs JWT

| Cookie | JWT |
|---|---|
| Browser apps | APIs |
| Cookie stored | Token stored |
| Automatic sending | Manual sending |
| Session-based | Stateless |

---

# Simple Meaning

```text
JWT Authentication
    ↓
Client Sends Token
```

---

# 3. OAuth

---

# What is OAuth?

OAuth allows login using:
- Google
- Facebook
- GitHub
- Microsoft

without sharing password.

---

# Example

```text
Login with Google
```

---

# OAuth Flow

```text
User Clicks Google Login
        ↓
Redirect To Google
        ↓
Google Verifies User
        ↓
Google Sends Access Token
        ↓
Application Logs User In
```

---

# IMPORTANT

Application never sees:
- Google password

---

# OAuth Purpose

Used for:
- Third-party login
- External authentication

---

# OAuth Example

```text
Login with Google
Login with Facebook
```

---

# Program.cs Example

```cs
builder.Services
    .AddAuthentication()
    .AddGoogle(options =>
{
    options.ClientId = "CLIENT_ID";

    options.ClientSecret = "SECRET";
});
```

---

# OAuth Features

- Secure login
- External providers
- No password storage

---

# Simple Meaning

```text
OAuth
    ↓
Login Using Another Company
```

---

# 4. OpenID Connect

---

# What is OpenID Connect?

OpenID Connect (OIDC) is identity layer built on top of OAuth.

---

# Purpose

Used for:
- User identity verification
- Login systems

---

# Difference

| OAuth | OpenID Connect |
|---|---|
| Authorization | Authentication |
| Access APIs | Verify user identity |

---

# OpenID Connect Flow

```text
User Login
      ↓
Identity Provider Verifies User
      ↓
ID Token Generated
      ↓
Application Reads User Identity
```

---

# Identity Providers

- Google
- Microsoft
- Auth0
- Okta

---

# Example

```text
Login with Google Account
```

---

# Program.cs Example

```cs
builder.Services
    .AddAuthentication()
    .AddOpenIdConnect(options =>
{
    
});
```

---

# OpenID Connect Features

- User identity verification
- Single Sign-On (SSO)
- Enterprise login systems

---

# OAuth vs OpenID Connect

| OAuth | OpenID Connect |
|---|---|
| Access permission | User login |
| Access token | ID token |
| API access | Authentication |

---

# Authentication Pipeline

```text
Client Request
        ↓
UseAuthentication()
        ↓
Validate User
        ↓
Create User Identity
        ↓
UseAuthorization()
        ↓
Check Permissions
        ↓
Controller Executes
```

---

# Authentication Components

| Component | Purpose |
|---|---|
| UseAuthentication | Validate user |
| Claims | User information |
| Cookie | Store login |
| JWT | API token |
| OAuth | External login |
| OpenID Connect | Identity verification |

---

# Claims

---

# What are Claims?

Claims store user information.

---

# Example Claims

```text
User Id
Username
Role
Email
```

---

# Example

```cs
new Claim(ClaimTypes.Name, "Deep")
```

---

# Access Current User

```cs
User.Identity.Name
```

---

# Authorization Example

```cs
[Authorize(Roles = "Admin")]
```

---

# Meaning

Only Admin users allowed.

---

# Common Authentication Errors

| Error | Meaning |
|---|---|
| 401 Unauthorized | Not logged in |
| 403 Forbidden | No permission |

---

# Real-Life Analogy

| Authentication Concept | Real Life |
|---|---|
| Authentication | ID Card Check |
| Authorization | Room Permission |
| Cookie | Visitor Pass |
| JWT Token | Digital ID Card |
| OAuth | Login Using Google |
| OpenID Connect | Identity Verification |