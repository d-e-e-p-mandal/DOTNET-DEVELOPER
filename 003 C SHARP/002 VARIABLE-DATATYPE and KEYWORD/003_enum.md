# C# Enum Complete Notes (Simple & Interview Ready)

# What is Enum?

An **enum (Enumeration)** is a special **value type** in C# that represents a **fixed set of named constants**.

Instead of allowing any value (like a string or int), it allows only predefined values.

---

# Why Use Enum?

Without enum:

```csharp
public class Employee
{
    public string Status { get; set; }
}
```

Usage

```csharp
employee.Status = "Active";
employee.Status = "Inactive";
employee.Status = "Wrong";      // Allowed ❌
employee.Status = "ABC";        // Allowed ❌
```

Problems

- Typing mistakes
- Any value is allowed
- No compile-time safety
- Difficult to maintain

---

With enum

```csharp
public enum Status
{
    Active,
    Inactive,
    Pending
}

public class Employee
{
    public Status Status { get; set; }
}
```

Usage

```csharp
employee.Status = Status.Active;
employee.Status = Status.Pending;
```

Invalid

```csharp
employee.Status = "Active";   // ❌ Error
employee.Status = "ABC";      // ❌ Error
```

Only predefined values are allowed.

---

# Real Life Examples

Status

```csharp
public enum Status
{
    Active,
    Inactive,
    Pending
}
```

Gender

```csharp
public enum Gender
{
    Male,
    Female,
    Other
}
```

Role

```csharp
public enum Role
{
    Admin,
    Employee,
    Customer
}
```

Priority

```csharp
public enum Priority
{
    Low,
    Medium,
    High
}
```

Payment Status

```csharp
public enum PaymentStatus
{
    Pending,
    Success,
    Failed
}
```

---

# Enum Storage

By default enum stores integer values.

```csharp
public enum Status
{
    Active,
    Inactive,
    Pending
}
```

Internally

```text
Active     = 0
Inactive   = 1
Pending    = 2
```

---

# Custom Integer Values

```csharp
public enum Status
{
    ACT = 10,
    INA = 20,
    PEN = 30
}
```

Internally

```text
ACT = 10
INA = 20
PEN = 30
```

---

# Enum Underlying Types

Default

```csharp
enum Status
{
    Active,
    Inactive
}
```

Underlying type

```
int
```

Other supported types

```csharp
public enum Status : byte
{
    Active = 1,
    Inactive = 2
}
```

Supported types

- byte
- sbyte
- short
- ushort
- int (default)
- uint
- long
- ulong

---

# Can Enum Store String?

No.

Wrong

```csharp
public enum Status
{
    Active = "Active"
}
```

Compiler Error

Enums can only have integral numeric values.

---

# Basic Example

```csharp
public enum Status
{
    Active,
    Inactive,
    Pending
}

Status s = Status.Active;
```

---

# Printing Enum

```csharp
Console.WriteLine(s);
```

Output

```
Active
```

Reason

`Console.WriteLine()` automatically calls `ToString()` for enums.

Equivalent to

```csharp
Console.WriteLine(s.ToString());
```

Output

```
Active
```

---

# Get Integer Value

```csharp
Console.WriteLine((int)s);
```

Output

```
0
```

For custom values

```csharp
public enum Status
{
    ACT = 10,
    INA = 20,
    PEN = 30
}

Status s = Status.ACT;

Console.WriteLine((int)s);
```

Output

```
10
```

---

# ToString()

Converts enum to its **name**.

```csharp
Status s = Status.ACT;

string value = s.ToString();
```

Result

```
ACT
```

Not

```
10
```

---

# Convert Enum To Int

```csharp
Status s = Status.ACT;

int value = (int)s;
```

Result

```
10
```

---

# Convert Int To Enum

```csharp
Status s = (Status)20;
```

Output

```
INA
```

---

# Convert String To Enum

```csharp
Status s = Enum.Parse<Status>("ACT");
```

Output

```
ACT
```

Internally

```
"ACT"
      │
      ▼
Status.ACT
```

---

# Safe Conversion

```csharp
if(Enum.TryParse("ACT", out Status status))
{
    Console.WriteLine(status);
}
```

Output

```
ACT
```

Invalid input

```csharp
Enum.TryParse("ABC", out Status status)
```

Returns

```
False
```

No exception occurs.

---

# Get All Enum Values

```csharp
foreach(Status s in Enum.GetValues(typeof(Status)))
{
    Console.WriteLine(s);
}
```

Output

```
Active
Inactive
Pending
```

---

# Get All Enum Names

```csharp
foreach(string s in Enum.GetNames(typeof(Status)))
{
    Console.WriteLine(s);
}
```

Output

```
Active
Inactive
Pending
```

---

# Enum.IsDefined()

Checks whether a value exists in the enum.

```csharp
bool valid = Enum.IsDefined(typeof(Status),20);
```

Output

```
True
```

Example

```csharp
bool valid = Enum.IsDefined(typeof(Status),50);
```

Output

```
False
```

---

# Important Interview Question

Can enum store invalid values?

Yes.

```csharp
Status s = (Status)50;
```

This compiles.

Output

```
50
```

Why?

Because enum is stored as an integer internally.

Validate before use

```csharp
if(Enum.IsDefined(typeof(Status),50))
{
    Console.WriteLine("Valid");
}
else
{
    Console.WriteLine("Invalid");
}
```

Output

```
Invalid
```

---

# Description Attribute

```csharp
using System.ComponentModel;

public enum Status
{
    [Description("Active")]
    ACT,

    [Description("Inactive")]
    INA,

    [Description("Pending")]
    PEN
}
```

Purpose

Adds extra descriptive text.

It does **NOT** change the enum value.

Example

```csharp
Console.WriteLine(Status.ACT);
```

Output

```
ACT
```

Example

```csharp
Console.WriteLine(Status.ACT.ToString());
```

Output

```
ACT
```

The description `"Active"` is not returned automatically.

---

# Reading Description

```csharp
public static string GetDescription(Status status)
{
    var field = status.GetType().GetField(status.ToString());

    var attribute =
        (DescriptionAttribute)Attribute.GetCustomAttribute(
            field,
            typeof(DescriptionAttribute));

    return attribute?.Description ?? status.ToString();
}
```

Usage

```csharp
Console.WriteLine(GetDescription(Status.ACT));
```

Output

```
Active
```

---

# EF Core Default Storage

Model

```csharp
public enum Status
{
    ACT = 10,
    INA = 20,
    PEN = 30
}

public class Employee
{
    public int Id { get; set; }

    public Status Status { get; set; }
}
```

EF Core stores

```
10
```

Database column

```sql
STATUS NUMBER
```

Default behavior:

**Enums are stored as integers.**

---

# Store Enum as String

Configure Value Converter

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>()
        .Property(e => e.Status)
        .HasConversion<string>();
}
```

Now EF Core stores

```
ACT
```

instead of

```
10
```

Database column

```sql
STATUS VARCHAR2(20)
```

---

# What Does HasConversion<string>() Do?

Without converter

```
Status.ACT
      │
      ▼
10
      │
Database
```

With converter

```
Status.ACT
      │
      ▼
ToString()
      │
      ▼
"ACT"
      │
Database
      │
      ▼
EF Core converts back
      │
      ▼
Status.ACT
```

No manual conversion is required.

---

# Oracle Database

Store Integer

```sql
STATUS NUMBER
```

Stores

```
10
20
30
```

Store String

```sql
STATUS VARCHAR2(20)
```

Stores

```
ACT
INA
PEN
```

---

# Prevent Invalid Database Values

Without constraint

```sql
INSERT INTO EMPLOYEE VALUES(1,50);
```

Works ❌

---

Add CHECK constraint

```sql
ALTER TABLE EMPLOYEE
ADD CONSTRAINT CHK_STATUS
CHECK (STATUS IN (10,20,30));
```

Now

Allowed

```
10
20
30
```

Rejected

```
50
```

Oracle Error

```
ORA-02290
```

---

# EF Core CHECK Constraint

```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>()
        .ToTable(t =>
            t.HasCheckConstraint(
                "CK_Employee_Status",
                "STATUS IN (10,20,30)"
            ));
}
```

Migration generates

```sql
CHECK (STATUS IN (10,20,30))
```

---

# Best Practices

✅ Use enum when values are fixed.

Examples

- Status
- Gender
- Role
- Payment Status
- Priority
- Order Status

Don't use enum for

- Name
- Address
- City
- Email
- Description

---

# Advantages

- Type-safe
- IntelliSense support
- Better readability
- Easier maintenance
- Avoids spelling mistakes
- Better than magic numbers
- Faster comparisons

---

# Disadvantages

- Cannot store strings directly
- Values are fixed
- Invalid integers can still be cast
- Requires validation with `Enum.IsDefined()`
- Database should use a `CHECK` constraint for full protection

---

# Quick Revision

| Operation | Code | Result |
|-----------|------|--------|
| Print enum | `Console.WriteLine(s)` | `ACT` |
| Enum → String | `s.ToString()` | `"ACT"` |
| Enum → Int | `(int)s` | `10` |
| Int → Enum | `(Status)10` | `Status.ACT` |
| String → Enum | `Enum.Parse<Status>("ACT")` | `Status.ACT` |
| Safe parse | `Enum.TryParse()` | Returns `true`/`false` |
| Validate | `Enum.IsDefined()` | Checks valid value |
| Default EF Core storage | `Status` | `10` |
| EF Core string storage | `HasConversion<string>()` | `ACT` |
| Oracle NUMBER | Stores | `10` |
| Oracle VARCHAR2 | Stores | `ACT` |
| Database protection | `CHECK` constraint | Prevents invalid values |


---
---

# Interview Questions

### What is enum?

A value type representing a fixed set of named constants.

---

### Default underlying type?

```
int
```

---

### Can enum store string?

No.

---

### Can enum inherit class?

No.

---

### Can enum implement interface?

No.

---

### Can enum have methods?

No.

---

### Can enum have constructors?

No.

---

### Can enum have duplicate values?

Yes.

Example

```csharp
public enum Status
{
    Active=1,
    Enabled=1
}
```

---

### Can enum contain negative values?

Yes.

```csharp
public enum Status
{
    Failed=-1,
    Success=1
}
```

---

### Can enum start from any value?

Yes.

```csharp
public enum Status
{
    One=100,
    Two=200
}
```

---

### How to validate enum?

```csharp
Enum.IsDefined(typeof(Status),value)
```

---

### How to convert enum to string?

```csharp
status.ToString()
```

---

### How to convert enum to int?

```csharp
(int)status
```

---

### How to convert int to enum?

```csharp
(Status)value
```

---

### How to convert string to enum?

```csharp
Enum.Parse<Status>("Active")
```

---

# Summary

| Feature | Enum |
|----------|------|
| Stores | Integer |
| Default Type | int |
| Can Store String | No |
| ToString() | Enum Name |
| Int Conversion | (int)Enum |
| String Conversion | ToString() |
| Validation | Enum.IsDefined() |
| Oracle NUMBER | Store Integer |
| Oracle VARCHAR2 | Store ToString() |
| Automatic CHECK Constraint | No |
| Database Protection | CHECK Constraint |
| Best For | Fixed values |