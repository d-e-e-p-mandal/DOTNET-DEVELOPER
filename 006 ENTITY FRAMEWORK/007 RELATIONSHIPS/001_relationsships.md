# ⚫ 7. RELATIONSHIPS

---

# What are Relationships?

Relationships define how tables are connected to each other.

---

# Example

```text
Employee
    ↓
Department
```

An employee belongs to a department.

---

# Why Relationships?

Used to:
- Connect tables
- Reduce duplicate data
- Maintain data integrity

---

# Relationship Types

- One to One
- One to Many
- Many to Many

---

# 1. One to One Relationship

---

# Meaning

One record is connected to only one record.

---

# Example

```text
Person
   ↔
Passport
```

One person has one passport.

One passport belongs to one person.

---

# Database

```text
Persons
-------
Id
Name

Passports
---------
Id
PassportNumber
PersonId
```

---

# Entity Classes

## Person

```cs
public class Person
{
    public int Id { get; set; }

    public string Name { get; set; }

    public Passport Passport
    {
        get;
        set;
    }
}
```

---

## Passport

```cs
public class Passport
{
    public int Id { get; set; }

    public string PassportNumber
    {
        get;
        set;
    }

    public int PersonId
    {
        get;
        set;
    }

    public Person Person
    {
        get;
        set;
    }
}
```

---

# Relationship

```text
One Person
      ↔
One Passport
```

---

# 2. One to Many Relationship

---

# Meaning

One record can have many related records.

---

# Example

```text
Department
      ↓
Many Employees
```

One department contains many employees.

---

# Database

```text
Departments
-----------
Id
Name

Employees
---------
Id
Name
DepartmentId
```

---

# Entity Classes

## Department

```cs
public class Department
{
    public int Id { get; set; }

    public string Name { get; set; }

    public ICollection<Employee>
        Employees
    {
        get;
        set;
    }
}
```

---

## Employee

```cs
public class Employee
{
    public int Id { get; set; }

    public string Name { get; set; }

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

# Relationship

```text
One Department
        ↓
Many Employees
```

---

# Most Common Relationship

```text
One To Many
```

used in industry.

---

# Examples

```text
Department → Employees

Customer → Orders

Teacher → Students
```

---

# 3. Many to Many Relationship

---

# Meaning

Many records related to many records.

---

# Example

```text
Students
      ↔
Courses
```

One student can join many courses.

One course can have many students.

---

# Database

```text
Students
--------
Id
Name

Courses
-------
Id
Title

StudentCourses
--------------
StudentId
CourseId
```

---

# Entity Classes

## Student

```cs
public class Student
{
    public int Id { get; set; }

    public string Name { get; set; }

    public ICollection<Course>
        Courses
    {
        get;
        set;
    }
}
```

---

## Course

```cs
public class Course
{
    public int Id { get; set; }

    public string Title
    {
        get;
        set;
    }

    public ICollection<Student>
        Students
    {
        get;
        set;
    }
}
```

---

# Relationship

```text
Many Students
        ↔
Many Courses
```

---

# Navigation Properties

---

# What are Navigation Properties?

Properties used to navigate between related entities.

---

# Simple Meaning

```text
Object Reference
To Related Table
```

---

# Example

```cs
public Department Department
{
    get;
    set;
}
```

---

# Meaning

Employee can access Department.

---

# Example

```cs
employee.Department.Name
```

---

# Collection Navigation

```cs
public ICollection<Employee>
    Employees
{
    get;
    set;
}
```

---

# Meaning

Department can access all employees.

---

# Navigation Property Types

## Reference Navigation

```cs
public Department Department
{
    get;
    set;
}
```

One object.

---

## Collection Navigation

```cs
public ICollection<Employee>
    Employees
{
    get;
    set;
}
```

Many objects.

---

# Foreign Keys

---

# What is Foreign Key?

Foreign Key connects two tables.

---

# Simple Meaning

```text
Foreign Key
      ↓
Reference To Parent Table
```

---

# Example

```cs
public int DepartmentId
{
    get;
    set;
}
```

---

# Meaning

Employee belongs to Department.

---

# Database

```text
Employees
-----------
Id
Name
DepartmentId
```

---

# Relationship

```text
Department.Id
      ↓
Employee.DepartmentId
```

---

# SQL Example

```sql
FOREIGN KEY
(DepartmentId)
REFERENCES Departments(Id)
```

---

# Cascade Delete

---

# What is Cascade Delete?

Automatically deletes child records when parent record is deleted.

---

# Example

```text
Department
      ↓
Employees
```

Delete Department.

---

# Cascade Delete Result

```text
Department Deleted
      ↓
All Related Employees Deleted
```

---

# Example

Before

```text
Department
----------
1 HR

Employees
----------
1 Rahul 1
2 Deep  1
```

---

# Delete Department

```text
Department Id = 1
```

---

# After

```text
Department Deleted

Employees Deleted
```

---

# Benefit

No orphan records.

---

# Orphan Record Meaning

```text
Employee Exists
But Department Does Not Exist
```

---

# Configure Cascade Delete

```cs
modelBuilder.Entity<Employee>()
    .HasOne(e => e.Department)
    .WithMany(d => d.Employees)
    .HasForeignKey(
        e => e.DepartmentId)
    .OnDelete(
        DeleteBehavior.Cascade);
```

---

# Common Delete Behaviors

## Cascade

```text
Delete Parent
      ↓
Delete Children
```

---

## Restrict

```text
Cannot Delete Parent
If Children Exist
```

---

## SetNull

```text
Delete Parent
      ↓
Foreign Key = NULL
```

---

# Complete Relationship Flow

```text
Department
      ↓
Foreign Key
      ↓
Employee
      ↓
Navigation Property
      ↓
Access Related Data
```

---

# Relationship Summary

| Relationship | Example |
|-------------|----------|
| One to One | Person → Passport |
| One to Many | Department → Employees |
| Many to Many | Students ↔ Courses |

---

# Important Terms

| Term | Meaning |
|--------|----------|
| Navigation Property | Access Related Entity |
| Foreign Key | Connect Tables |
| Reference Navigation | One Object |
| Collection Navigation | Many Objects |
| Cascade Delete | Delete Related Records |

---

# Real-Life Analogy

| EF Core | Real Life |
|----------|-----------|
| One to One | Person ↔ Passport |
| One to Many | Department → Employees |
| Many to Many | Students ↔ Courses |
| Foreign Key | Relationship ID |
| Navigation Property | Direct Access |
| Cascade Delete | Remove Entire Family Record |

---

# Simple Understanding

```text
One To One
     ↓
1 ↔ 1

One To Many
     ↓
1 → Many

Many To Many
     ↓
Many ↔ Many

Foreign Key
     ↓
Connect Tables

Navigation Property
     ↓
Access Related Data

Cascade Delete
     ↓
Delete Parent
Delete Children
```