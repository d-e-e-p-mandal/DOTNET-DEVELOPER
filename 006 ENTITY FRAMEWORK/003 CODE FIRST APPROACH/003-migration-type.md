# EF Core Code First - EnsureCreated() vs Database.Migrate() vs `dotnet ef database update`

## Introduction

In **Entity Framework Core (Code First)**, there are **three common ways** to create or update a database.

1. **EnsureCreated()**
2. **Database.Migrate()**
3. **dotnet ef database update (Command Line)**

> **Important**
>
> - `EnsureCreated()` **does not use migrations**.
> - `Database.Migrate()` **uses migrations**.
> - `dotnet ef database update` **also uses migrations**.
> - `Database.Migrate()` and `dotnet ef database update` perform the **same job** (apply pending migrations). The difference is **where they run**.

---

# 1. EnsureCreated()

## What is EnsureCreated()?

`EnsureCreated()` checks whether the database exists.

- If the database does **not** exist
  - Creates the database
  - Creates all tables from the current entity models

- If the database **already exists**
  - Does **nothing**

It **does not compare models**, **does not update tables**, and **does not use migrations**.

---

## Syntax

```csharp
context.Database.EnsureCreated();
```

---

## Workflow

```
Application Starts
        │
        ▼
EnsureCreated()
        │
        ▼
Database Exists?
      │
 ┌────┴─────┐
 │          │
No         Yes
 │          │
 ▼          ▼
Create     Do Nothing
Database
Tables
```

---

## Example

### Employee Model

```csharp
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

Run

```csharp
context.Database.EnsureCreated();
```

Database

```
Employee
---------
Id
Name
```

---

## Later

Suppose you modify the model.

```csharp
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }

    public string Email { get; set; }
}
```

Run again

```csharp
context.Database.EnsureCreated();
```

Result

```
Employee

Id
Name
```

Email column is **NOT** created.

Reason

```
Database already exists

↓

EnsureCreated()

↓

Do Nothing
```

---

## Files Created

None

No Migration folder

No Migration files

No History table

---

## Advantages

- Very simple
- Automatically creates database
- Automatically creates tables
- No migration files
- Good for testing
- Good for prototypes

---

## Disadvantages

- Cannot update schema
- Cannot add columns
- Cannot remove columns
- Cannot rename columns
- Cannot track changes
- Not suitable for production

---

## Best Used For

- Learning EF Core
- Testing
- Prototype applications
- Temporary database

---

# 2. Database.Migrate()

## What is Database.Migrate()?

`Database.Migrate()` automatically applies all **pending migrations** when the application starts.

Unlike `EnsureCreated()`, it supports updating the database.

---

## Syntax

```csharp
context.Database.Migrate();
```

---

## Requirement

Before using

```csharp
Database.Migrate()
```

You must create migrations.

---

## Step 1

Create Model

```csharp
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

---

## Step 2

Create migration

```bash
dotnet ef migrations add InitialCreate
```

Generated

```
Migrations

InitialCreate.cs

InitialCreate.Designer.cs

ApplicationDbContextModelSnapshot.cs
```

---

## Step 3

Run Application

```csharp
context.Database.Migrate();
```

Result

```
Database

Employee

Id
Name
```

---

## Later

Add new property

```csharp
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }

    public string Email { get; set; }
}
```

Create Migration

```bash
dotnet ef migrations add AddEmployeeEmail
```

Run Application

```csharp
context.Database.Migrate();
```

Database becomes

```
Employee

Id
Name
Email
```

Existing data remains.

---

## Workflow

```
Application Starts

↓

Database.Migrate()

↓

Check __EFMigrationsHistory

↓

Pending Migration?

↓

Yes

↓

Apply Migration

↓

Update History Table
```

---

## Files Required

```
Migrations

InitialCreate.cs

InitialCreate.Designer.cs

ApplicationDbContextModelSnapshot.cs

AddEmployeeEmail.cs

AddEmployeeEmail.Designer.cs
```

---

## Advantages

- Automatically updates database
- Automatically adds new columns
- Automatically creates new tables
- Migration history maintained
- Production ready
- Works with SQL Server
- Works with Oracle
- Works with MySQL
- Works with PostgreSQL
- Works with SQLite

---

## Disadvantages

- Requires migration files
- Slightly more setup

---

## Best Used For

- Production
- IIS Deployment
- Enterprise Projects
- Large Applications

---

# 3. dotnet ef database update

## What is it?

Instead of updating the database from application code, EF Core updates it from the command line.

It performs exactly the same work as

```csharp
context.Database.Migrate();
```

Difference

```
Database.Migrate()

↓

Application updates database automatically.
```

```
dotnet ef database update

↓

Developer updates database manually.
```

---

## Command

```bash
dotnet ef database update
```

---

## Workflow

```
Create Model

↓

Create Migration

↓

Run

dotnet ef database update

↓

Database Updated
```

---

## Example

Model

```csharp
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

Create Migration

```bash
dotnet ef migrations add InitialCreate
```

Update Database

```bash
dotnet ef database update
```

Database

```
Employee

Id
Name
```

---

## Add New Column

Model

```csharp
public string Email { get; set; }
```

Create Migration

```bash
dotnet ef migrations add AddEmployeeEmail
```

Update Database

```bash
dotnet ef database update
```

Database

```
Employee

Id
Name
Email
```

---

## Advantages

- Manual control
- Good for development
- Good for CI/CD
- No application startup required

---

## Disadvantages

- Must remember to run command
- Easy to forget

---

## Best Used For

- Local Development
- Manual Deployment
- CI/CD Pipeline

---

# Migration Files

Running

```bash
dotnet ef migrations add InitialCreate
```

creates

```
Migrations
│
├── InitialCreate.cs
├── InitialCreate.Designer.cs
└── ApplicationDbContextModelSnapshot.cs
```

---

## InitialCreate.cs

Contains operations like

```csharp
CreateTable(
    "Employee"
);
```

---

## InitialCreate.Designer.cs

Stores metadata for the migration.

Usually developers do not edit this file.

---

## ApplicationDbContextModelSnapshot.cs

Stores the latest snapshot of the model.

EF Core compares this snapshot with the current model to generate future migrations.

---

# Adding Another Migration

Model

```csharp
public string Email { get; set; }
```

Command

```bash
dotnet ef migrations add AddEmployeeEmail
```

Generated

```
AddEmployeeEmail.cs

AddEmployeeEmail.Designer.cs
```

Contains

```csharp
AddColumn(
    "Email"
);
```

---

# __EFMigrationsHistory

When using migrations, EF Core automatically creates

```
__EFMigrationsHistory
```

Example

| MigrationId |
|-------------|
| InitialCreate |
| AddEmployeeEmail |

Purpose

Stores every migration already applied to the database.

---

## How EF Core Uses It

Application Starts

↓

Read

```
__EFMigrationsHistory
```

↓

Already Applied?

```
InitialCreate
```

↓

Skip

↓

Pending?

```
AddEmployeeEmail
```

↓

Run Migration

↓

Update History

---

Without this table EF Core would not know which migrations have already been executed.

---

# Common EF Core Commands

## Create First Migration

```bash
dotnet ef migrations add InitialCreate
```

---

## Create New Migration

```bash
dotnet ef migrations add AddEmployeeEmail
```

---

## Update Database

```bash
dotnet ef database update
```

---

## Remove Last Migration

```bash
dotnet ef migrations remove
```

---

## List All Migrations

```bash
dotnet ef migrations list
```

---

## Generate SQL Script

```bash
dotnet ef migrations script
```

---

# Workflow Comparison

## EnsureCreated()

```
Create Model

↓

Run Application

↓

EnsureCreated()

↓

Database Created

↓

Change Model

↓

Run Again

↓

Nothing Happens
```

---

## Database.Migrate()

```
Create Model

↓

Create Migration

↓

Run Application

↓

Database.Migrate()

↓

Database Created

↓

Modify Model

↓

Create Migration

↓

Run Application

↓

Only Pending Changes Applied
```

---

## dotnet ef database update

```
Create Model

↓

Create Migration

↓

Run Command

↓

Database Updated

↓

Modify Model

↓

Create Migration

↓

Run Command Again

↓

Only Pending Changes Applied
```

---

# Difference Table

| Feature | EnsureCreated() | Database.Migrate() | dotnet ef database update |
|----------|-----------------|--------------------|---------------------------|
| Uses Migrations | ❌ No | ✅ Yes | ✅ Yes |
| Creates Database | ✅ Yes | ✅ Yes* | ✅ Yes* |
| Creates Tables | ✅ Yes | ✅ Yes | ✅ Yes |
| Updates Existing Tables | ❌ No | ✅ Yes | ✅ Yes |
| Adds New Columns | ❌ No | ✅ Yes | ✅ Yes |
| Removes Columns | ❌ No | ✅ Yes (via migration) | ✅ Yes (via migration) |
| Migration Files Required | ❌ No | ✅ Yes | ✅ Yes |
| Creates `__EFMigrationsHistory` | ❌ No | ✅ Yes | ✅ Yes |
| Automatic at Application Startup | ✅ Yes | ✅ Yes | ❌ No |
| Manual Command Needed | ❌ No | ❌ No | ✅ Yes |
| Best For | Testing / Prototype | Production | Development / CI-CD |

> \* Creating the database itself depends on the EF Core provider and database permissions. In SQL Server this is often possible if the login has permission; in Oracle, applications commonly connect to an existing schema rather than creating a new database.