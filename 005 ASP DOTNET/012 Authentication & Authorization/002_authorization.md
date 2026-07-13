# Authorization in ASP.NET Core

---

# What is Authorization?

Authorization checks:

```text
What can user access?
```

---

# Purpose

Used for:
- Permission control
- Access restriction
- Security

---

# Simple Meaning

```text
Authorization = Access Permission Checking
```

---

# Example

```text
User Logged In
      ↓
Can User Access Admin Panel?
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
"Can you enter admin room?"
```

---

# Authorization Flow

```text
User Login
      ↓
Authentication Success
      ↓
Authorization Checks Permissions
      ↓
Allow or Deny Access
```

---

# Authorization Middleware

---

# Program.cs

```cs
app.UseAuthentication();

app.UseAuthorization();
```

---

# IMPORTANT ORDER

Authentication must come first.

---

# Why?

Because:
- First identify user
- Then check permissions

---

# Authorization Types

- Role-Based Authorization
- Policy-Based Authorization
- Claims-Based Authorization

---

# Authorization Attribute

```cs
[Authorize]
```

---

# Purpose

Allows only authenticated users.

---

# Example

```cs
[Authorize]
public IActionResult Dashboard()
{
    return Ok("Secure Page");
}
```

---

# Without Login

```text
401 Unauthorized
```

---

# With Login

```text
200 OK
```

---

# 1. Role-Based Authorization

---

# What is Role-Based Authorization?

Access control based on user roles.

---

# Example Roles

- Admin
- Manager
- Employee

---

# Purpose

Used to:
- Restrict pages
- Restrict APIs
- Secure admin areas

---

# Example

```cs
[Authorize(Roles = "Admin")]
public IActionResult AdminPanel()
{
    return Ok("Admin Access");
}
```

---

# Meaning

Only users with:

```text
Admin Role
```

can access.

---

# Flow

```text
User Login
      ↓
Check User Role
      ↓
Role Matches ?
   ↓          ↓
 YES          NO
 ↓             ↓
Access      403 Forbidden
```

---

# Multiple Roles

```cs
[Authorize(Roles = "Admin,Manager")]
```

---

# Meaning

Either:
- Admin
- Manager

can access.

---

# Adding Role in Claims

```cs
new Claim(ClaimTypes.Role, "Admin")
```

---

# Example Login

```cs
var claims = new List<Claim>
{
    new Claim(ClaimTypes.Name, "Deep"),

    new Claim(ClaimTypes.Role, "Admin")
};
```

---

# Access Current Role

```cs
User.IsInRole("Admin")
```

---

# Example

```cs
if(User.IsInRole("Admin"))
{

}
```

---

# Common Result

| Condition | Result |
|---|---|
| Logged In + Correct Role | Access |
| Logged In + Wrong Role | 403 Forbidden |
| Not Logged In | 401 Unauthorized |

---

# Simple Meaning

```text
Role-Based Authorization
    ↓
Access Based On User Role
```

---

# 2. Policy-Based Authorization

---

# What is Policy-Based Authorization?

Authorization using custom rules/policies.

---

# Purpose

Used for:
- Complex authorization
- Custom business rules

---

# Example

```text
Only users older than 18
```

---

# Create Policy

## Program.cs

```cs
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy(
        "AdminOnly",
        policy =>
            policy.RequireRole("Admin"));
});
```

---

# Explanation

---

# AddPolicy()

Creates custom policy.

---

# "AdminOnly"

Policy name.

---

# RequireRole()

Requires specific role.

---

# Use Policy

```cs
[Authorize(Policy = "AdminOnly")]
public IActionResult Dashboard()
{
    return Ok();
}
```

---

# Flow

```text
Request
   ↓
Policy Executes
   ↓
Condition Valid ?
   ↓          ↓
 YES          NO
 ↓             ↓
Access      Forbidden
```

---

# Multiple Requirements

```cs
options.AddPolicy(
    "ManagerPolicy",
    policy =>
    {
        policy.RequireRole("Manager");

        policy.RequireClaim(
            "Department",
            "IT");
    });
```

---

# Meaning

User must:
- Be Manager
- Department = IT

---

# Benefits

- Flexible authorization
- Reusable rules
- Complex conditions

---

# Simple Meaning

```text
Policy-Based Authorization
    ↓
Custom Access Rules
```

---

# 3. Claims-Based Authorization

---

# What are Claims?

Claims are user information stored after login.

---

# Example Claims

- User Id
- Email
- Role
- Department

---

# Example Claim

```cs
new Claim("Department", "IT")
```

---

# What is Claims-Based Authorization?

Authorization using claim values.

---

# Example

```text
Department = IT
```

Only IT users allowed.

---

# Add Claims

```cs
var claims = new List<Claim>
{
    new Claim(ClaimTypes.Name, "Deep"),

    new Claim("Department", "IT")
};
```

---

# Policy Using Claim

```cs
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy(
        "ITOnly",
        policy =>
            policy.RequireClaim(
                "Department",
                "IT"));
});
```

---

# Use Policy

```cs
[Authorize(Policy = "ITOnly")]
public IActionResult ITDashboard()
{
    return Ok();
}
```

---

# Flow

```text
Request
   ↓
Check Claim
   ↓
Claim Valid ?
   ↓         ↓
 YES         NO
 ↓            ↓
Access      Forbidden
```

---

# Access User Claims

```cs
User.Claims
```

---

# Example

```cs
var department =
    User.FindFirst("Department")?.Value;
```

---

# Claims vs Roles

| Claims | Roles |
|---|---|
| Detailed user info | User category |
| Flexible | Simple |
| Department, Age | Admin, User |

---

# Authorization Status Codes

| Status Code | Meaning |
|---|---|
| 401 Unauthorized | User not logged in |
| 403 Forbidden | No permission |

---

# Authorization Pipeline

```text
Client Request
        ↓
UseAuthentication()
        ↓
User Identified
        ↓
UseAuthorization()
        ↓
Check Roles/Policies/Claims
        ↓
Controller Executes
```

---

# Complete Example

## Program.cs

```cs
builder.Services.AddAuthorization(options =>
{
    options.AddPolicy(
        "AdminOnly",
        policy =>
            policy.RequireRole("Admin"));
});
```

---

# Controller

```cs
[Authorize(Policy = "AdminOnly")]
public IActionResult Admin()
{
    return Ok("Admin Panel");
}
```

---

# Real-Life Analogy

| Authorization Concept | Real Life |
|---|---|
| Authorization | Permission Check |
| Role | Job Position |
| Policy | Company Rule |
| Claims | Employee Information |
| Admin Role | Manager Access |
| Forbidden | Access Denied |

---

# SIMPLE UNDERSTANDING

```text
Authentication
    ↓
"Who are you?"

Authorization
    ↓
"What can you access?"
```

---

# COMPLETE FLOW

```text
User Login
      ↓
Authentication Success
      ↓
Claims & Roles Created
      ↓
Authorization Checks
      ↓
Access Granted or Denied
```