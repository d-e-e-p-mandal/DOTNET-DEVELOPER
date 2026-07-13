# 🔴 6. CRUD OPERATIONS

CRUD stands for:

```text
C = Create
R = Read
U = Update
D = Delete
```

Used for database operations.

---

# CRUD Flow

```text
Application
      ↓
DbContext
      ↓
DbSet
      ↓
Database
```

---

# 1. Insert Data

---

# What is Insert?

Used to add new record into database.

---

# Example

```cs
var employee = new Employee
{
    Name = "Deep",
    Salary = 50000
};

_context.Employees.Add(employee);

_context.SaveChanges();
```

---

# Flow

```text
Create Object
      ↓
Add()
      ↓
SaveChanges()
      ↓
Record Inserted
```

---

# Add Multiple Records

```cs
_context.Employees.AddRange(
    employee1,
    employee2
);

_context.SaveChanges();
```

---

# 2. Select Data

---

# What is Select?

Used to retrieve data from database.

---

# Get All Records

```cs
var employees =
    _context.Employees.ToList();
```

---

# SQL

```sql
SELECT * FROM Employees
```

---

# Get Single Record

```cs
var employee =
    _context.Employees
        .FirstOrDefault(
            x => x.Id == 1);
```

---

# SQL

```sql
SELECT *
FROM Employees
WHERE Id = 1
```

---

# Flow

```text
Query
    ↓
Database
    ↓
Records Returned
```

---

# 3. Update Data

---

# What is Update?

Used to modify existing records.

---

# Example

```cs
var employee =
    _context.Employees.Find(1);

employee.Name = "Rahul";

_context.SaveChanges();
```

---

# Flow

```text
Find Record
      ↓
Modify Data
      ↓
SaveChanges()
      ↓
Record Updated
```

---

# Using Update()

```cs
_context.Employees.Update(employee);

_context.SaveChanges();
```

---

# 4. Delete Data

---

# What is Delete?

Used to remove record.

---

# Example

```cs
var employee =
    _context.Employees.Find(1);

_context.Employees.Remove(employee);

_context.SaveChanges();
```

---

# Flow

```text
Find Record
      ↓
Remove()
      ↓
SaveChanges()
      ↓
Record Deleted
```

---

# Delete Multiple Records

```cs
_context.Employees.RemoveRange(
    employees
);

_context.SaveChanges();
```

---

# SaveChanges()

---

# What is SaveChanges()?

Used to save all changes to database.

---

# Example

```cs
_context.SaveChanges();
```

---

# Purpose

Applies:

- Insert
- Update
- Delete

operations.

---

# Without SaveChanges()

```cs
_context.Employees.Add(employee);
```

Record NOT saved.

---

# Required

```cs
_context.SaveChanges();
```

---

# Flow

```text
Add / Update / Delete
          ↓
SaveChanges()
          ↓
Database Updated
```

---

# SaveChangesAsync()

---

# What is SaveChangesAsync()?

Asynchronous version of SaveChanges().

---

# Example

```cs
await _context.SaveChangesAsync();
```

---

# Purpose

Used in:
- Web APIs
- Large applications
- Async programming

---

# Example

```cs
_context.Employees.Add(employee);

await _context.SaveChangesAsync();
```

---

# Advantage

```text
Does Not Block Thread
```

---

# Industry Recommendation

```cs
SaveChangesAsync()
```

preferred in ASP.NET Core.

---

# Find()

---

# What is Find()?

Used to find record by Primary Key.

---

# Example

```cs
var employee =
    _context.Employees.Find(1);
```

---

# Meaning

```text
Find Employee
Where Id = 1
```

---

# SQL

```sql
SELECT *
FROM Employees
WHERE Id = 1
```

---

# Return Type

```cs
Employee
```

or

```text
null
```

if not found.

---

# Best Use

```text
Search By Primary Key
```

---

# FirstOrDefault()

---

# What is FirstOrDefault()?

Returns first matching record.

---

# Example

```cs
var employee =
    _context.Employees
        .FirstOrDefault(
            x => x.Name == "Deep");
```

---

# SQL

```sql
SELECT TOP 1 *
FROM Employees
WHERE Name = 'Deep'
```

---

# Result

Returns:

```text
First Matching Record
```

or

```text
null
```

---

# Best Use

```text
Get First Matching Record
```

---

# SingleOrDefault()

---

# What is SingleOrDefault()?

Returns exactly one record.

---

# Example

```cs
var employee =
    _context.Employees
        .SingleOrDefault(
            x => x.Email ==
                 "deep@gmail.com");
```

---

# Result

### One Record

```text
Returns Record
```

---

### No Record

```text
Returns null
```

---

### Multiple Records

```text
Throws Exception
```

---

# Best Use

```text
When Data Must Be Unique
```

Examples:
- Email
- Aadhaar Number
- Username

---

# Difference

| Method | Purpose |
|----------|----------|
| Find() | Search By Primary Key |
| FirstOrDefault() | First Matching Record |
| SingleOrDefault() | Exactly One Record |

---

# Example Comparison

## Find()

```cs
_context.Employees.Find(1);
```

Search by:

```text
Primary Key Only
```

---

## FirstOrDefault()

```cs
_context.Employees
    .FirstOrDefault(
        x => x.Name == "Deep");
```

Returns:

```text
First Match
```

---

## SingleOrDefault()

```cs
_context.Employees
    .SingleOrDefault(
        x => x.Email ==
             "deep@gmail.com");
```

Returns:

```text
Only One Match
```

Throws error if multiple found.

---

# Complete CRUD Example

```cs
// INSERT
_context.Employees.Add(employee);
await _context.SaveChangesAsync();

// SELECT
var employees =
    await _context.Employees.ToListAsync();

// UPDATE
var emp =
    await _context.Employees.FindAsync(1);

emp.Name = "Rahul";

await _context.SaveChangesAsync();

// DELETE
_context.Employees.Remove(emp);

await _context.SaveChangesAsync();
```

---

# Simple Understanding

```text
Add()
     ↓
Insert Record

ToList()
     ↓
Get Records

Update()
     ↓
Modify Record

Remove()
     ↓
Delete Record

SaveChanges()
     ↓
Apply Changes

Find()
     ↓
Search By Primary Key

FirstOrDefault()
     ↓
First Matching Record

SingleOrDefault()
     ↓
Exactly One Record
```