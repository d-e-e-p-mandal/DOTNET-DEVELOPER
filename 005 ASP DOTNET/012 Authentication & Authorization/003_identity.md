# 🔹 ASP.NET Core Identity

---

# What is ASP.NET Core Identity?

ASP.NET Core Identity is built-in authentication and user management system.

Used for:
- User registration
- Login
- Logout
- Password hashing
- Role management
- Authentication

---

# Simple Meaning

```text
ASP.NET Core Identity
    ↓
Complete Login System
```

---

# Features

- User management
- Secure passwords
- Role management
- Authentication
- Authorization
- Cookie login

---

# Identity Flow

```text
User Registers
      ↓
Password Hashed
      ↓
User Stored In Database
      ↓
User Login
      ↓
Cookie Created
      ↓
User Authenticated
```

---

# Identity Main Components

| Component | Purpose |
|---|---|
| UserManager | User operations |
| SignInManager | Login/logout |
| IdentityUser | User table |
| IdentityRole | Role table |

---

# Identity Database Tables

Identity automatically creates tables.

---

# Common Tables

| Table | Purpose |
|---|---|
| AspNetUsers | Store users |
| AspNetRoles | Store roles |
| AspNetUserRoles | User-role mapping |
| AspNetUserClaims | User claims |

---

# Install Identity Package

```bash
dotnet add package
Microsoft.AspNetCore.Identity.EntityFrameworkCore
```

---

# Configure Identity

---

# Program.cs

```cs
builder.Services
    .AddIdentity<
        IdentityUser,
        IdentityRole>()
    .AddEntityFrameworkStores<AppDbContext>()
    .AddDefaultTokenProviders();
```

---

# Explanation

---

# AddIdentity()

Enables Identity system.

---

# IdentityUser

Represents users table.

---

# IdentityRole

Represents roles table.

---

# AddEntityFrameworkStores()

Stores Identity data in database.

---

# AddDefaultTokenProviders()

Used for:
- Reset password
- Email confirmation

---

# Add Authentication Middleware

```cs
app.UseAuthentication();

app.UseAuthorization();
```

---

# 1. User Management

---

# What is User Management?

Managing users inside application.

---

# Includes

- Create user
- Update user
- Delete user
- Find user

---

# UserManager

Used for user operations.

---

# Inject UserManager

```cs
private readonly UserManager<IdentityUser>
    _userManager;

public AccountController(
    UserManager<IdentityUser> userManager)
{
    _userManager = userManager;
}
```

---

# Create User

```cs
var user = new IdentityUser
{
    UserName = "deep",

    Email = "deep@gmail.com"
};
```

---

# Save User

```cs
await _userManager.CreateAsync(
    user,
    "Password@123");
```

---

# What Happens?

---

# Step 1

Identity creates user.

---

# Step 2

Password hashed automatically.

---

# Step 3

User saved in:
- AspNetUsers table

---

# Find User

```cs
var user =
    await _userManager
        .FindByEmailAsync(
            "deep@gmail.com");
```

---

# Delete User

```cs
await _userManager.DeleteAsync(user);
```

---

# Update User

```cs
user.Email = "new@gmail.com";

await _userManager.UpdateAsync(user);
```

---

# Simple Meaning

```text
UserManager
    ↓
Controls Users
```

---

# 2. Registration

---

# What is Registration?

Creating new user account.

---

# Registration Flow

```text
User Enters Details
        ↓
Identity Validates Data
        ↓
Password Hashed
        ↓
User Saved In Database
```

---

# Register Model

```cs
public class RegisterModel
{
    public string Email { get; set; }

    public string Password { get; set; }
}
```

---

# Registration API

```cs
[HttpPost]
public async Task<IActionResult>
    Register(RegisterModel model)
{
    var user = new IdentityUser
    {
        UserName = model.Email,

        Email = model.Email
    };

    var result =
        await _userManager.CreateAsync(
            user,
            model.Password);

    if(result.Succeeded)
    {
        return Ok("User Created");
    }

    return BadRequest(result.Errors);
}
```

---

# Explanation

---

# CreateAsync()

Creates new user.

---

# Password Automatically Hashed

Identity never stores plain password.

---

# Registration Result

| Result | Meaning |
|---|---|
| Success | User created |
| Failed | Validation error |

---

# Common Registration Errors

- Weak password
- Duplicate email
- Invalid email

---

# 3. Login

---

# What is Login?

Verifying user credentials.

---

# Login Flow

```text
User Enters Email & Password
        ↓
Identity Verifies Password
        ↓
Authentication Cookie Created
        ↓
User Logged In
```

---

# SignInManager

Used for login/logout operations.

---

# Inject SignInManager

```cs
private readonly
    SignInManager<IdentityUser>
    _signInManager;
```

---

# Login Model

```cs
public class LoginModel
{
    public string Email { get; set; }

    public string Password { get; set; }
}
```

---

# Login API

```cs
[HttpPost]
public async Task<IActionResult>
    Login(LoginModel model)
{
    var result =
        await _signInManager
            .PasswordSignInAsync(
                model.Email,
                model.Password,
                false,
                false);

    if(result.Succeeded)
    {
        return Ok("Login Success");
    }

    return Unauthorized();
}
```

---

# Explanation

---

# PasswordSignInAsync()

Checks:
- User exists
- Password correct

---

# If Valid

Identity creates:
- Authentication cookie

---

# If Invalid

Returns:

```text
401 Unauthorized
```

---

# Simple Meaning

```text
Login
    ↓
Verify User + Create Cookie
```

---

# 4. Logout

---

# What is Logout?

Removes user authentication.

---

# Logout API

```cs
[HttpPost]
public async Task<IActionResult>
    Logout()
{
    await _signInManager.SignOutAsync();

    return Ok("Logged Out");
}
```

---

# What Happens?

---

# Step 1

Authentication cookie removed.

---

# Step 2

User becomes unauthenticated.

---

# After Logout

Protected pages cannot access.

---

# Simple Meaning

```text
Logout
    ↓
Remove User Login Session
```

---

# 5. Password Hashing

---

# What is Password Hashing?

Converts password into secure encrypted format.

---

# IMPORTANT

Identity NEVER stores:
- Plain password

---

# Example

---

# User Password

```text
Password@123
```

---

# Stored In Database

```text
AQAAAAEAACcQAAAA...
```

---

# Why Hashing Important?

Protects passwords from:
- Hackers
- Database leaks

---

# Identity Automatically Hashes Password

```cs
await _userManager.CreateAsync(
    user,
    password);
```

---

# Password Verification

During login:
- Identity compares hash values

---

# PasswordHasher

```cs
PasswordHasher<IdentityUser>
```

used internally.

---

# Simple Meaning

```text
Password Hashing
    ↓
Convert Password Into Secure Code
```

---

# 6. Role Management

---

# What is Role Management?

Managing user roles.

---

# Example Roles

- Admin
- Manager
- Employee

---

# IdentityRole

Represents role table.

---

# RoleManager

Used for role operations.

---

# Inject RoleManager

```cs
private readonly
    RoleManager<IdentityRole>
    _roleManager;
```

---

# Create Role

```cs
await _roleManager.CreateAsync(
    new IdentityRole("Admin"));
```

---

# Add User To Role

```cs
await _userManager.AddToRoleAsync(
    user,
    "Admin");
```

---

# Check User Role

```cs
await _userManager.IsInRoleAsync(
    user,
    "Admin");
```

---

# Protect Controller

```cs
[Authorize(Roles = "Admin")]
public IActionResult AdminPanel()
{
    return Ok();
}
```

---

# Meaning

Only Admin users allowed.

---

# Role Flow

```text
User Login
      ↓
Identity Reads User Roles
      ↓
Authorization Checks Role
      ↓
Access Allowed or Denied
```

---

# Identity Authentication Flow

```text
User Registers
      ↓
Password Hashed
      ↓
User Stored In Database
      ↓
User Login
      ↓
Cookie Created
      ↓
Authentication Success
      ↓
Authorization Checks Roles
```

---

# Identity Classes Summary

| Class | Purpose |
|---|---|
| UserManager | User operations |
| SignInManager | Login/logout |
| RoleManager | Role management |
| IdentityUser | User model |
| IdentityRole | Role model |

---

# Identity Security Features

- Password hashing
- Secure cookies
- Role management
- Claims support
- Token providers

---

# Common Identity Features

| Feature | Purpose |
|---|---|
| Register | Create user |
| Login | Authenticate user |
| Logout | Remove authentication |
| Roles | Permission management |
| Claims | User information |
| Password Hashing | Secure passwords |

---

# Real-Life Analogy

| Identity Part | Real Life |
|---|---|
| Registration | Create Bank Account |
| Login | ATM PIN Verification |
| Logout | Remove Access Card |
| Password Hashing | Secret Locker |
| Role | Job Position |
| UserManager | Employee Manager |
| SignInManager | Security Desk |
| RoleManager | HR Department |

---

# SIMPLE UNDERSTANDING

```text
ASP.NET Core Identity
        ↓
Complete Authentication System
```

---

# COMPLETE FLOW

```text
User Registers
      ↓
Identity Stores User
      ↓
Password Hashed
      ↓
User Logs In
      ↓
Cookie Created
      ↓
User Authenticated
      ↓
Authorization Checks Roles
      ↓
Access Granted
```