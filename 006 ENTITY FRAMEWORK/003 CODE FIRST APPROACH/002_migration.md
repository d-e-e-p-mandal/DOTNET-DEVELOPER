# Migrations in Entity Framework Core

**What is Migration?**
- Migration is a feature that tracks database changes.
- It generate system files in database.

Used for:
- Creating tables
- Updating tables
- Modifying columns
- Managing database schema


# Migration Flow

```text
Entity Class Changed
        ↓
Add Migration
        ↓
Migration File Created
        ↓
Update Database
        ↓
Database Updated
```

## Example

**Entity:**

```cs
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

**Create Migration:**
```bash
dotnet ef migrations add InitialCreate
```

**Update Database:**
```bash
dotnet ef database update
```

**Result:**
- Employee Table Created


# Migration Folder : Automatically created

```text
Project
│
├── Migrations
│     ├── InitialCreate.cs
│     ├── InitialCreate.Designer.cs
│     └── AppDbContextModelSnapshot.cs
```

**Purpose:**
- Stores database change history.

**Migration Process:**

```text
Entity Class
      ↓
Migration File
      ↓
Database
```

------

# Add Migration ; (One table add)

### What is Add Migration?
- Creates migration files based on model changes.

### Command

```bash
dotnet ef migrations add InitialCreate
```

**Meaning:**
- Create New Migration

### Example:

```bash
dotnet ef migrations add CreateEmployeeTable
```

# Result

```text
Migrations/
      CreateEmployeeTable.cs
```

- created.


### What Happens?

- EF compares and generates migration.

```text
Current Models
        VS
Previous Snapshot
```


### Flow

```text
Entity Changed
      ↓
Add Migration
      ↓
Migration File Created
```

---

# 2. Update Database

# What is Update Database?

- Applies migration to actual database.

### Command

```bash
dotnet ef database update
```

**Meaning:**
- Apply Migration To Database

### Example:
```bash
dotnet ef database update
```

### Result

```text
Database Created
Tables Created
Columns Added
```

### Flow

```text
Migration Exists
       ↓
Update Database
       ↓
Database Updated
```


# Update Specific Migration

```bash
dotnet ef database update InitialCreate
```

---

# Meaning

Database moves to:

```text
InitialCreate Migration
```

state.

---

# Update To Zero : Remove All Migrations From Database

```bash
dotnet ef database update 0
```

# Tables removed.

---

# 3. Remove Migration

**What is Remove Migration?**
- Removes last migration.

## Command

```bash
dotnet ef migrations remove
```

**Meaning:**
- Delete Last Migration

# Example

**Before:**

```text
Migrations
│
├── InitialCreate
├── AddDepartment
```

**After:**
```text
Migrations
│
├── InitialCreate
```

##### IMPORTANT: Works only for: `Last Migration`



### Use Case
When:
- Wrong migration created
- Model mistake fixed


# Flow

```text
Wrong Migration
      ↓
Remove Migration
      ↓
Migration Deleted
```

---

# 4. List Migrations

**What is List Migration?**
- Shows all migrations.


# Command

```bash
dotnet ef migrations list
```

# Output
```
InitialCreate
AddDepartment
AddEmployeeAddress
```

**Purpose:**

Used to check:

- Migration history
- Applied migrations
- Available migrations

# Flow

```text
Run Command
      ↓
Show All Migrations
```

-----

# Simple Understanding

```text
Add Migration
      ↓
Create Database Changes

Update Database
      ↓
Apply Changes

Remove Migration
      ↓
Delete Last Change

List Migrations
      ↓
Show History

Drop Database
      ↓
Delete Database
```


--------------


## Remove :
Yes, but only if the last migration has not been applied to the database.

Case 1: Migration not applied to the database ✅

M1 → M2 → M3

Run:

dotnet ef migrations remove

Result:

M1 → M2

Run again:

dotnet ef migrations remove

Result:

M1

This works correctly.

⸻

Case 2: Migration already applied to the database ⚠️

If M3 has already been applied using:

dotnet ef database update

then:

dotnet ef migrations remove

will fail with an error similar to:

The migration has already been applied to the database.

First, roll the database back:

dotnet ef database update M2

Then remove the migration:

dotnet ef migrations remove
