# MODEL CONFIGURATION

# What is Model Configuration?

Model Configuration is used to define how Entity Classes map to database tables.

Used for:
- Primary Keys
- Column Names
- Table Names
- Relationships
- Validation Rules

# Two Ways

1. Data Annotations
2. Fluent API


---

# Data Annotations

**What are Data Annotations?**
- Attributes written above class properties.

Used to configure:
- Tables
- Columns
- Validation
- Keys

---

### Namespace

```cs
using System.ComponentModel.DataAnnotations;

using System.ComponentModel.DataAnnotations.Schema;
```


**Example Entity:**

```cs
public class Employee
{
    [Key]
    public int Id { get; set; }

    [Required]
    [MaxLength(100)]
    public string Name { get; set; }
}
```


# 1. [Key]

Defines Primary Key.

**Example:**

```cs
[Key]
public int EmployeeId { get; set; }
```

**Result:**
- EmployeeId = Primary Key


**SQL:**

```sql
EmployeeId INT PRIMARY KEY
```


# 2. [Required]

- Field cannot be NULL.

**Example:**

```cs
[Required]
public string Name { get; set; }
```

**Result:**
- Name Required


**SQL:**

```sql
Name NVARCHAR(MAX) NOT NULL
```

# 3. [MaxLength]

- Sets maximum length.

**Example:**

```cs
[MaxLength(50)]
public string Name { get; set; }
```


**Result:**
- Maximum 50 Characters


**SQL:**

```sql
Name NVARCHAR(50)
```


# 4. [Table]

- Specify table name.

**Example:**

```cs
[Table("Employees")]
public class Employee
{

}
```

**Result:**

```text
Table Name = Employees
```


**Without Table Attribute:**
- `Employee` table created.

**With Table Attribute:**
- `Employees` table created.



# 5. [Column]

- Specify column name.

**Example:**

```cs
[Column("EmployeeName")]
public string Name { get; set; }
```

**Result:**

```text
Property Name = Name

Column Name = EmployeeName
```


**SQL:**

```sql
EmployeeName NVARCHAR(MAX)
```

# 6. [NotMapped]

---


Exclude property from database.

---

**Example:**

```cs
[NotMapped]
public int Age
{
    get;
    set;
}
```

**Result:**

```text
Age Column Not Created
```

# Used For

- Calculated fields
- Temporary properties


**Example:**

```cs
[NotMapped]
public string FullName
{
    get;
    set;
}
```


---

# Fluent API

# What is Fluent API?

Configuration written inside:

```cs
OnModelCreating()
```

method.


# Simple Meaning

```text
Configure Database Using Code
```

---

# Why Use Fluent API?

Used when:
- Data Annotations not enough
- Complex relationships
- Advanced configuration

---

# Location

```cs
AppDbContext
```

---

**Example:**

```cs
protected override void
OnModelCreating(
    ModelBuilder modelBuilder)
{

}
```

---

# What is OnModelCreating()?

Method called when EF creates model.

Used for:
- Table configuration
- Relationships
- Constraints

---

**Example:**

```cs
protected override void
OnModelCreating(
    ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>();
}
```

---

# 1. HasKey()

---


Define Primary Key.

---

**Example:**

```cs
modelBuilder.Entity<Employee>()
    .HasKey(e => e.Id);
```

---

# Meaning

```text
Id = Primary Key
```

---

# Equivalent

```cs
[Key]
public int Id { get; set; }
```

---

# 2. HasOne()

---


Define One Relationship.

---

**Example:**

```cs
modelBuilder.Entity<Employee>()
    .HasOne(e => e.Department);
```

---

# Meaning

```text
Employee Has One Department
```

---

# Relationship

```text
Employee
     ↓
Department
```

---

# 3. HasMany()

---


Define Many Relationship.

---

**Example:**

```cs
modelBuilder.Entity<Department>()
    .HasMany(d => d.Employees);
```

---

# Meaning

```text
Department Has Many Employees
```

---

# Relationship

```text
Department
      ↓
Many Employees
```

---

# One-to-Many Example

## Employee

```cs
public class Employee
{
    public int Id { get; set; }

    public int DepartmentId
    {
        get;
        set;
    }

    public Department Department
    {
        get;
        set;
    }
}
```

---

## Department

```cs
public class Department
{
    public int Id { get; set; }

    public ICollection<Employee>
        Employees
    {
        get;
        set;
    }
}
```

---

## Fluent API

```cs
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>()
        .HasOne(e => e.Department)
        .WithMany(d => d.Employees)
        .HasForeignKey(e => e.DepartmentId);
}
```

---

# Relationship Meaning

```text
One Department
        ↓
Many Employees
```

---

# Complete Flow

```text
Entity Class
       ↓
Data Annotations
       OR
Fluent API
       ↓
Migration
       ↓
Database Structure Created
```

---

# Data Annotations vs Fluent API

| Data Annotation | Fluent API |
|-----------------|------------|
| Easy | Advanced |
| Inside Model | Inside DbContext |
| Simple Config | Complex Config |
| Less Flexible | More Flexible |

---