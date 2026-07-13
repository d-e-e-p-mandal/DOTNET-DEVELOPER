# Entity Framework Fluent API Configuration

**Namespace:**
```cs
using Microsoft.EntityFrameworkCore;
```
⸻

**What is Fluent API?**
- Fluent API is used to configure entities and database mappings inside:

```cs
protected override void OnModelCreating(
    ModelBuilder modelBuilder)
{
}
```

**Complete Example:**

```cs
protected override void OnModelCreating(
    ModelBuilder modelBuilder)
{
    modelBuilder.Entity<Employee>()
        .HasKey(e => e.Id);
    modelBuilder.Entity<Employee>()
        .Property(e => e.Name)
        .HasMaxLength(100)
        .IsRequired();
    modelBuilder.Entity<Employee>()
        .ToTable("Employees");
}
```
⸻

### Entity Configuration

### Entity()

Select entity for configuration.
```cs
modelBuilder.Entity<Employee>();
```

### Table Configuration

### ToTable()

Specify table name.
```cs
modelBuilder.Entity<Employee>()
    .ToTable("Employees");
```
Equivalent:

[Table("Employees")]


### Primary Key Configuration

### HasKey()
- Define primary key.

```cs
modelBuilder.Entity<Employee>()
    .HasKey(e => e.Id);
```
Equivalent:
[Key]


Composite Key
```cs
modelBuilder.Entity<Product>()
    .HasKey(p => new
    {
        p.Id,
        p.Code
    });
```
Equivalent:
[PrimaryKey(nameof(Id), nameof(Code))]



### Column Configuration

## HasColumnName()

- Custom column name.

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Name)
    .HasColumnName("EmployeeName");
```
Equivalent:
[Column("EmployeeName")]


### HasColumnType()

- Custom SQL datatype.

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Name)
    .HasColumnType("varchar(50)");
```
Equivalent:

[Column(TypeName="varchar(50)")]

⸻

### HasPrecision()

- Decimal precision.

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Salary)
    .HasPrecision(18,2);
```
Equivalent:
[Precision(18,2)]

⸻

### IsUnicode()
- Unicode configuration.

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Code)
    .IsUnicode(false);
```
Equivalent:

[Unicode(false)]

⸻

### Validation Configuration

### IsRequired()

- Not Null.

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Name)
    .IsRequired();
```
Equivalent:

[Required]


### HasMaxLength()

Maximum length.

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Name)
    .HasMaxLength(100);
```
Equivalent:
[MaxLength(100)]

⸻

Ignore Configuration

### Ignore()

- Ignore property.

```cs
modelBuilder.Entity<Employee>()
    .Ignore(e => e.Age);
```
Equivalent:

[NotMapped]

⸻

Index Configuration

### HasIndex()

Create index.
```cs
modelBuilder.Entity<Employee>()
    .HasIndex(e => e.Email);
```
Equivalent:
[Index(nameof(Email))]


Unique Index
```cs
modelBuilder.Entity<Employee>()
    .HasIndex(e => e.Email)
    .IsUnique();
```
Equivalent:

[Index(nameof(Email), IsUnique = true)]

⸻

## One To One Relationship

HasOne + WithOne
```cs
modelBuilder.Entity<Person>()
    .HasOne(p => p.Passport)
    .WithOne(p => p.Person)
    .HasForeignKey<Passport>(
        p => p.PersonId);
```
⸻

One To Many Relationship

HasOne + WithMany
```cs
modelBuilder.Entity<Employee>()
    .HasOne(e => e.Department)
    .WithMany(d => d.Employees)
    .HasForeignKey(
        e => e.DepartmentId);
```
⸻

### Many To Many Relationship

```cs
modelBuilder.Entity<Student>()
    .HasMany(s => s.Courses)
    .WithMany(c => c.Students);
```
⸻

Relationship Methods

### HasOne()

- One reference.
```cs
.HasOne(e => e.Department)
```
⸻

### WithOne()

- One related entity.
.WithOne()

⸻

HasMany()

Many related entities.

.HasMany(d => d.Employees)

⸻

WithMany()

Many related entities.

.WithMany()

⸻

### HasForeignKey()

- Configure foreign key.
```cs
.HasForeignKey(
    e => e.DepartmentId)
```
Equivalent:

[ForeignKey]

⸻

Cascade Delete

### OnDelete()

Configure delete behavior.
```cs
modelBuilder.Entity<Employee>()
    .HasOne(e => e.Department)
    .WithMany(d => d.Employees)
    .HasForeignKey(
        e => e.DepartmentId)
    .OnDelete(
        DeleteBehavior.Cascade);
```
⸻

Delete Behaviors
```cs
DeleteBehavior.Cascade
DeleteBehavior.Restrict
DeleteBehavior.SetNull
DeleteBehavior.NoAction
```

- Default Values

### HasDefaultValue()
```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Status)
    .HasDefaultValue("Active");
```

### HasDefaultValueSql()
```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.CreatedDate)
    .HasDefaultValueSql("GETDATE()");
```

- Computed Columns

### HasComputedColumnSql()
```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.FullName)
    .HasComputedColumnSql(
        "[FirstName] + ' ' + [LastName]");
```
⸻

Concurrency

### IsRowVersion()

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.RowVersion)
    .IsRowVersion();
```
Equivalent:

[Timestamp]

⸻

Database Generated Values

### ValueGeneratedOnAdd()

```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Id)
    .ValueGeneratedOnAdd();
```
Equivalent:

[DatabaseGenerated(DatabaseGeneratedOption.Identity)]

⸻

### ValueGeneratedNever()
```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.Id)
    .ValueGeneratedNever();
```
⸻

ValueGeneratedOnUpdate()
```cs
modelBuilder.Entity<Employee>()
    .Property(e => e.LastModified)
    .ValueGeneratedOnUpdate();
```

- Seed Data

### HasData()
```cs
modelBuilder.Entity<Employee>()
    .HasData(
        new Employee
        {
            Id = 1,
            Name = "Deep"
        });
```
⸻

Complete Classification

Table Configuration

ToTable()

⸻

Key Configuration

HasKey()

⸻

Column Configuration

HasColumnName()
HasColumnType()
HasPrecision()
IsUnicode()

⸻

Validation

IsRequired()
HasMaxLength()

⸻

Ignore

Ignore()

⸻

Index

HasIndex()
IsUnique()

⸻

Relationships

HasOne()
WithOne()
HasMany()
WithMany()
HasForeignKey()

⸻

Delete Behavior

OnDelete()

⸻

Default Values

HasDefaultValue()
HasDefaultValueSql()

⸻

Computed Columns

HasComputedColumnSql()

⸻

Database Generated

ValueGeneratedOnAdd()
ValueGeneratedNever()
ValueGeneratedOnUpdate()

⸻

Concurrency

IsRowVersion()

⸻

Seed Data

HasData()