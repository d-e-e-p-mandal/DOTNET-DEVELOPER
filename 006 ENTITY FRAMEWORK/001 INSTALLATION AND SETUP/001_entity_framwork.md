# Entity Framework (EF)

## Introduction

### What is Entity Framework?
- Entity Framework (EF) is Microsoft's ORM(Object Oriented Model) framework for .NET.
- It helps developers work with databases using C# objects instead of writing SQL queries manually.


### ORM (Object Relational Mapping)

**ORM converts:**
```text
C# Objects
      ↕
Database Tables
```

**Example:**
```cs
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```
↓
```text
Employee Table
```


### Advantages of Entity Framework

- Less SQL writing
- Faster development
- Easy CRUD operations
- Automatic database mapping
- Supports LINQ queries
- Database migrations support


### Features of Entity Framework

- ORM Support
- LINQ Queries
- Change Tracking
- Migrations
- Relationship Management
- Code First
- Database First


# Types of Entity Framework

## Entity Framework 6 (EF6)

- Older version
- Works mainly with .NET Framework
- Windows-focused
- Not actively developed much

**Example**

```text
ASP.NET MVC 5
.NET Framework 4.x
```

## Entity Framework Core (EF Core)

- Modern version
- Cross-platform
- Works with .NET Core / .NET 5+ / .NET 6+ / .NET 8+
- Better performance
- Actively developed by Microsoft

### Example

```text
ASP.NET Core
.NET 8
```

---

# Simple Difference

| EF6 | EF Core |
|------|---------|
| Old | Modern |
| .NET Framework | .NET Core / .NET 8 |
| Windows Mostly | Cross Platform |
| Slower | Faster |
| Less Features Updated | Actively Updated |

