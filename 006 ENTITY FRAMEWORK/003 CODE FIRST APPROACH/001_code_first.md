# CODE FIRST APPROACH (EF CORE)

# 1. Concept of Code First

Code First means:
- First we create C# classes  
- Then Entity Framework Core automatically creates the database


# Flow of Code First

```text
C# Classes → DbContext → Migration → Database
```


# Why Use Code First?

- No need to create database manually
- Database is generated automatically
- Easy to maintain
- Full control using code
- Mostly used in modern applications


# 2. Creating Models (Entities)

## What is a Model?

- Model represents a table in database

---

# Example

```csharp
public class Employee
{
    public int Id { get; set; }      // Primary Key
    public string Name { get; set; }
    public int Salary { get; set; }
}
```

---

# Explanation

| Property | Meaning |
|---|---|
| Id | Primary Key |
| Name | Employee Name |
| Salary | Employee Salary |

---

# Rules for Model Class

- Class must be `public`
- Must contain primary key
- Properties become table columns

---

# 3. Adding DbContext

## What is DbContext?

- DbContext connects application with database

- It manages:
- Tables
- Queries
- Save operations

---

# Example

```csharp
public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) {}

    public DbSet<Employee> Employees { get; set; }
}
```

---

# Explanation

| Code | Meaning |
|---|---|
| DbContext | Main EF Core class |
| DbSet<Employee> | Represents Employee table |
| Employees | Table name |

---

# 4. Migrations

# What is Migration?

- Migration is used to create or update database from model classes

---

# Migration 
- Creates database and tables

### What Happens Internally?

1. EF checks model classes
2. Creates migration file
3. Generates SQL queries
4. Creates database tables
