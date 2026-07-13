# DATABASE FIRST APPROACH (EF CORE)

# 1. Concept of Database First

Database First means:

- First database is already created  
- Then EF Core generates C# classes automatically

# Flow of Database First

```text
Database → EF Core → Models (Classes) → DbContext
```

---

# Example

Suppose database already contains:

- Table: Employees
- Columns:
  - Id
  - Name
  - Salary

- EF Core generates this class automatically:

```csharp
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

---

# 2. When to Use Database First?

## Use Database First When

- Database already exists
- Working on legacy projects
- Database designed by DBA
- Large enterprise systems
- Existing SQL Server projects

---

# 3. Steps to Use Database First

---

# Step 1: Install Required Packages

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

---

```bash
dotnet add package Microsoft.EntityFrameworkCore.Tools
```

---

# Purpose of Packages

| Package | Purpose |
|---|---|
| Microsoft.EntityFrameworkCore.SqlServer | Connects EF Core with SQL Server |
| Microsoft.EntityFrameworkCore.Tools | Provides migration and scaffold tools |

---

# Step 2: Scaffold Database

## What is Scaffold?

- Scaffold means generating C# classes from existing database

---

# Scaffold Command

```bash
dotnet ef dbcontext scaffold "Server=.;Database=TestDB;Trusted_Connection=True;" Microsoft.EntityFrameworkCore.SqlServer -o Models
```

---

# What This Command Does?

- Reads database tables
- Reads columns and relationships
- Creates:
  - Model classes
  - DbContext class

---

# 4. Generated Files

# Generated Entity Class

```csharp
public partial class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

---

# Generated DbContext

```csharp
public partial class TestDbContext : DbContext
{
    public virtual DbSet<Employee> Employees { get; set; }
}
```

---

# Explanation

| Code | Meaning |
|---|---|
| DbSet<Employee> | Represents Employees table |
| Employee | Entity class |
| TestDbContext | Main database context class |

---

# 5. Key Features of Database First

## Features

- Automatically generates code
- Uses existing database
- No need to create models manually
- Fast setup for old databases
- Supports large databases

---

# 6. Limitations of Database First

## Disadvantages

- Database changes require re-scaffolding
- Hard to customize generated code
- Custom code may be overwritten
- Less flexibility compared to Code First

---

# 7. Code First vs Database First

| Feature | Code First | Database First |
|---|---|---|
| Start Point | Code | Database |
| Main Control | Developer | Database |
| Flexibility | High | Medium |
| Best For | New Projects | Existing Databases |
| Model Creation | Manual | Automatic |

---

# 8. Important Scaffold Options

# Command Format

```bash
dotnet ef dbcontext scaffold "connection_string" provider -o Models -f
```

---

# Important Options

| Option | Purpose |
|---|---|
| -o | Output folder |
| -f | Force overwrite existing files |
| -t | Generate specific table only |

---

# Example Using Specific Table

```bash
dotnet ef dbcontext scaffold "connection_string" Microsoft.EntityFrameworkCore.SqlServer -o Models -t Employees
```

- Generates only Employees table model

---

# 9. Advantages of Database First

## Advantages

- Best for existing databases
- Faster development
- No need to design tables again
- Useful in enterprise applications

---

# 10. Simple Understanding

## Easy Difference

### Code First

```text
Code → Database
```

- First write C# code  
- Then database is created

---

### Database First

```text
Database → Code
```

- First database exists  
- Then EF Core creates code

---

# 🎯 FINAL SUMMARY

| Topic | Meaning |
|---|---|
| Database First | Create code from database |
| Scaffold | Generate models automatically |
| DbContext | Connects application with DB |
| Existing Database | Main requirement |
| Best For | Legacy and enterprise systems |

---

# Important Points to Remember

- Database First = Database → Code
- Uses Scaffold command
- Generates Models automatically
- Generates DbContext automatically
- Best for existing databases
- Re-scaffold needed after DB changes