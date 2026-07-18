# Seed Data

## What is Seed Data?

Seed Data means inserting initial/default data into the database automatically.

Simple Meaning:

```text
Default Data Added
When Database Is Created
```

---

## Why Seed Data Used?

Used to insert:

- Default Admin User
- Default Roles
- Sample Data
- Lookup Data
- Configuration Data

Examples:

```text
Admin User

Country List

Department List

Roles
```

---

## Example

Instead of manually inserting:

```sql
INSERT INTO Departments
VALUES ('IT');
```

every time,

EF Core can insert it automatically.

---

## Seed Data Flow

```text
Create Entity
      ↓
Configure Seed Data
      ↓
Add Migration
      ↓
Update Database
      ↓
Default Data Inserted
```

---

# Using HasData()

Seed data is configured inside:

```cs
OnModelCreating()
```

---

## Example Entity

```cs
public class Department
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

---

## Seed Data Configuration

```cs
protected override void OnModelCreating(
    ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Department>()
        .HasData(
            new Department
            {
                Id = 1,
                Name = "IT"
            },
            new Department
            {
                Id = 2,
                Name = "HR"
            }
        );
}
```

---

## Add Migration

```bash
dotnet ef migrations add SeedDepartmentData
```

---

## Update Database

```bash
dotnet ef database update
```

---

## Result

Table:

```text
Departments
```

Data:

| Id | Name |
|----|------|
| 1 | IT |
| 2 | HR |

Inserted automatically.

---

# Seed Multiple Records

```cs
modelBuilder.Entity<Employee>()
    .HasData(
        new Employee
        {
            Id = 1,
            Name = "Deep"
        },
        new Employee
        {
            Id = 2,
            Name = "John"
        }
    );
```

---

# Seed Data Rules

### Primary Key Required

```cs
Id = 1
```

Must be provided.

Correct:

```cs
new Department
{
    Id = 1,
    Name = "IT"
}
```

Wrong:

```cs
new Department
{
    Name = "IT"
}
```

---

### Migration Required

After changing seed data:

```bash
dotnet ef migrations add UpdateSeedData
```

Then:

```bash
dotnet ef database update
```

---

# Common Seed Data Examples

## Roles

```text
Admin

Manager

User
```

---

## Departments

```text
IT

HR

Finance
```

---

## Countries

```text
India

USA

UK
```

---

## Admin User

```text
admin@company.com
```

---

# Advantages

- Default data available immediately
- No manual insert required
- Consistent data across environments
- Useful for lookup tables

---

# Quick Revision

```text
Seed Data
      ↓
Default Database Data

Configured Using
      ↓
HasData()

Written Inside
      ↓
OnModelCreating()

Commands
      ↓
Add Migration

Database Update

Common Examples
      ↓
Roles
Departments
Countries
Admin User
```