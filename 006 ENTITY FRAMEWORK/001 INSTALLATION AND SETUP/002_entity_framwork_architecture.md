# Entity Framework Architecture

# What is Entity Framework Architecture?

Entity Framework works using three main components:

- Entity Classes
- DbSet
- DbContext

---

# Architecture Flow

```text
Controller / Service
          ↓
       DbContext
          ↓
        DbSet
          ↓
    Entity Classes
          ↓
      Database
```

---

# 1. Entity Classes

---

# What is Entity Class?

Entity Class represents a database table.

---

# Simple Meaning

```text
Entity Class = Database Table
```

---

# Example

```cs
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }

    public decimal Salary { get; set; }
}
```

---

# Database Table

```text
Employee
-------------------
Id
Name
Salary
```

---

# Explanation

| Property | Database Column |
|----------|----------------|
| Id | Id |
| Name | Name |
| Salary | Salary |

---

# Multiple Entity Classes

```cs
Employee
Department
Student
Product
Order
```

Each class becomes a table.

---

# 2. DbSet

---

# What is DbSet?

- DbSet represents a table inside DbContext.

```text
DbSet = Table Access Object
```

---

# Example

```cs
public DbSet<Employee> Employees
{
    get;
    set;
}
```

---

# Explanation

```text
Employees
     ↓
Employee Table
```

---

# CRUD Operations Through DbSet

## Insert

```cs
_context.Employees.Add(employee);
```

---

## Read

```cs
_context.Employees.ToList();
```

---

## Update

```cs
_context.Employees.Update(employee);
```

---

## Delete

```cs
_context.Employees.Remove(employee);
```

---

# Common Methods

```cs
Add()
AddRange()

Find()

Update()

Remove()
RemoveRange()

ToList()
```

---

# Simple Meaning

```text
DbSet
     ↓
Used To Access Table Data
```

---

# 3. DbContext

---

# What is DbContext?

DbContext is the main EF Core class.

Used for:
- Database connection
- Tracking changes
- Saving data
- Managing tables

---

# Simple Meaning

```text
DbContext = Database Manager
```

---

# Example

```cs
using Microsoft.EntityFrameworkCore;

public class AppDbContext
    : DbContext
{
    public AppDbContext(
        DbContextOptions<AppDbContext> options)
        : base(options)
    {

    }

    public DbSet<Employee> Employees
    {
        get;
        set;
    }
}
```

---

# Explanation

---

# AppDbContext

Custom database context.

---

# DbContext

Base EF Core class.

---

# DbSet<Employee>

Represents Employee table.

---

# SaveChanges()

```cs
_context.SaveChanges();
```

Used to save changes into database.

---

# Example

```cs
var employee =
    new Employee
    {
        Name = "Deep"
    };

_context.Employees.Add(employee);

_context.SaveChanges();
```

---

# Flow

```text
Create Object
      ↓
Add To DbSet
      ↓
SaveChanges()
      ↓
Database Updated
```

---

# Complete Example

## Entity

```cs
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

---

## DbContext

```cs
public class AppDbContext
    : DbContext
{
    public AppDbContext(
        DbContextOptions<AppDbContext> options)
        : base(options)
    {

    }

    public DbSet<Employee> Employees
    {
        get;
        set;
    }
}
```

---

## Program.cs

```cs
builder.Services.AddDbContext<AppDbContext>(
    options =>
        options.UseSqlServer(
            builder.Configuration
                   .GetConnectionString(
                       "DefaultConnection")));
```

---

# Complete Architecture Flow

```text
Employee Entity
       ↓
DbSet<Employee>
       ↓
AppDbContext
       ↓
SQL Server
```

---

# Summary Table

| Component | Purpose |
|------------|----------|
| Entity Class | Database Table |
| DbSet | Table Access |
| DbContext | Database Manager |

---

# Real-Life Analogy

| EF Core Part | Real Life |
|--------------|-----------|
| Entity Class | Form |
| DbSet | File Cabinet |
| DbContext | Office Manager |
| Database | Storage Room |

---
