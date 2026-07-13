# EF Commands

---

# First Time Database Creation

## Step 1: Create Migration

```bash
dotnet ef migrations add InitialCreate
```

### Purpose

Compare:

```text
Entity Classes
        +
DbContext
```

and generate migration files.

### Result

```text
Migrations Folder Created

InitialCreate.cs

InitialCreate.Designer.cs

AppDbContextModelSnapshot.cs
```

---

## Step 2: Create Database

```bash
dotnet ef database update
```

### Purpose

Apply migration to database.

### Result

```text
Database Created

Tables Created

Constraints Created
```

---

# Entity Changes:

Example:

```cs
public string Email { get; set; }
```

added to:

```cs
Employee
```

---

## Step 1: Add New Migration

```bash
dotnet ef migrations add AddEmployeeEmail
```

### Purpose

Generate migration for changes.

### Result

```text
New Migration File Created
```

---

## Step 2: Update Database

```bash
dotnet ef database update
```

### Purpose

Apply latest migration.

### Result

```text
Database Updated

New Column Added
```

---

# Create Migration

```bash
dotnet ef migrations add MigrationName
```

Example:

```bash
dotnet ef migrations add InitialCreate
```

Purpose:

```text
Create Migration File
```

---

# Update Database

```bash
dotnet ef database update
```

Purpose:

```text
Apply Pending Migrations

Create Database If Not Exists

Update Existing Database
```

---

# Update To Specific Migration

```bash
dotnet ef database update InitialCreate
```

Purpose:

```text
Rollback Or Move Database
To Specific Migration
```

---

# Remove Migration

```bash
dotnet ef migrations remove
```

Purpose:

```text
Delete Last Migration

Only If Not Applied
```

Result:

```text
Last Migration Removed
```

---

# List Migrations

```bash
dotnet ef migrations list
```

Purpose:

```text
Show All Migrations
```

Example:

```text
InitialCreate

AddEmployeeEmail

AddDepartmentTable
```

---

# Drop Database

```bash
dotnet ef database drop
```

Purpose:

```text
Delete Complete Database
```

Result:

```text
Database Deleted
```

---

# Confirmation

```text
Are you sure? (Y/N)
```

---

# Force Drop

```bash
dotnet ef database drop --force
```

Purpose:

```text
Delete Database
Without Confirmation
```

---

# Migration Lifecycle

```text
Create Entity
      ↓
Create DbContext
      ↓
Add Migration
      ↓
Migration File Created
      ↓
Database Update
      ↓
Database Created
      ↓
Modify Entity
      ↓
Add New Migration
      ↓
Migration File Created
      ↓
Database Update
      ↓
Database Updated
```

---

# Real Example

## Employee Entity

```cs
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

---

## Create Migration

```bash
dotnet ef migrations add InitialCreate
```

Result:

```text
Migration Files Created
```

---

## Create Database

```bash
dotnet ef database update
```

Result:

```text
Employee Table Created
```

---

## Modify Entity

```cs
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }

    public string Email { get; set; }
}
```

---

## Create New Migration

```bash
dotnet ef migrations add AddEmployeeEmail
```

Result:

```text
Email Column Migration Generated
```

---

## Update Database

```bash
dotnet ef database update
```

Result:

```text
Email Column Added To Database
```