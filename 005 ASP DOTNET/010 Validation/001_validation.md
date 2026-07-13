# What is Validation?

Validation checks whether input data is correct or not.


# Purpose
Used for:
- Prevent invalid data
- Improve security
- Ensure required fields


**Example:**

```text
Name Required
Age Must Be Positive
Email Must Be Valid
```

## Validation Types
- Data Annotations
- Client-Side Validation
- Server-Side Validation
- Custom Validation


# 1. Data Annotations

## What are Data Annotations?

Attributes used for validation.

## Namespace

```cs
using System.ComponentModel.DataAnnotations;
```

## Example Model

```cs
public class Employee
{
    public int Id { get; set; }

    [Required]
    public string Name { get; set; }

    [Range(18, 60)]
    public int Age { get; set; }

    [EmailAddress]
    public string Email { get; set; }
}
```

---

# Explanation

# [Required]
```cs
[Required]
```
- Field cannot be empty.

# [Range]

```cs
[Range(18, 60)]
```

- Age must be between: 18 & 60

# [EmailAddress]

```cs
[EmailAddress]
```

- Checks email format.

---

# Common Validation Attributes

| Attribute | Purpose |

|---|---|

| [Required] | Mandatory field |

| [Range] | Number range |

| [StringLength] | Text length |

| [EmailAddress] | Email validation |

| [Phone] | Phone validation |

---

# Validation Example

---

# Invalid Input

```json
{
  "age": 10
}
```

---

# Errors

```text
Name Required
Age Must Be Between 18 and 60
```

---

# 2. Client-Side Validation

---

# What is Client-Side Validation?

Validation runs in browser before request sent.

---

# Purpose
- Faster validation
- Better user experience

---

# Example

```text

Required field message shown immediately

```

---

# Flow

```text
User Input
      ↓
Browser Validation
      ↓
Error Message
```

---

# Used In
- MVC
- Razor Pages

# Example

```html

<input asp-for="Name" />

<span asp-validation-for="Name"></span>

```

---

# Validation Scripts

```html
<script src = "jquery.validate.min.js"></script>
```

---

# Simple Meaning

```text

Validation Before Sending Request

```

---

# 3. Server-Side Validation

---

# What is Server-Side Validation?

Validation runs on server after request received.

---

# IMPORTANT

Most secure validation.

---

# Example

```cs

[HttpPost]

public IActionResult Create(Employee employee)
{
    if (!ModelState.IsValid)
    {
        return BadRequest(ModelState);
    }
    return Ok(employee);
}
```

---

# ModelState.IsValid

Checks:

- Validation passed or not

---

# Flow

```text
Request Sent
      ↓
Server Receives Data
      ↓
Validation Runs
      ↓
   Valid ?
  ↓       ↓
 YES      NO
  ↓       ↓
Save     Error
```

---

# Validation Error Response

```json
{
  "errors": {
    "Name": [
      "The Name field is required."
    ]
  }
}
```

---

# Simple Meaning

```text
Validation On Server
```

---

# 4. Custom Validation

---

# What is Custom Validation?

Developer creates own validation rules.

---

# Example

```text

Name cannot be Admin

```

---

# Custom Validation Attribute

```cs

public class CustomNameAttribute : ValidationAttribute
{
    protected override ValidationResult IsValid( object value, ValidationContext validationContext)
    {
        if (value.ToString() == "Admin")
        {
            return new ValidationResult("Admin not allowed");
        }

        return ValidationResult.Success;
    }
}

```

---

# Use Custom Validation

```cs
public class Employee
{
    [CustomName]
    public string Name { get; set; }
}
```

---

# Result
If:
```text
Name = Admin
```

Error returned.

---

# Why Custom Validation?

Used for:
- Business rules
- Special validations

# Complete Validation Flow

```text
Request Data
      ↓
Model Binding
      ↓
Validation Runs
      ↓
    Valid ?
  ↓       ↓
 YES      NO
  ↓       ↓
Controller Error Response 
Executes
```

---

# Model Binding + Validation Flow

```text
Client Request
      ↓
Model Binding
      ↓
C# Object Created
      ↓
Validation Runs
      ↓
Controller Executes
```