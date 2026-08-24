
# Data Annotation Configuration Attributes

**Namespace:**
```cs
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
using Microsoft.EntityFrameworkCore;
```


**Complete Example:**
```cs
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;
using Microsoft.EntityFrameworkCore;
[Table("Employees")]
[Index(nameof(Email), IsUnique = true)]
public class Employee
{
    [Key]
    public int Id { get; set; }
    [Required]
    [MaxLength(100)]
    [Column("EmployeeName")]
    public string Name { get; set; }
    [Range(1000, 100000)]
    [Precision(18,2)]
    public decimal Salary { get; set; }
    [EmailAddress]
    public string Email { get; set; }
    [Phone]
    public string Mobile { get; set; }
    [NotMapped]
    public int Age { get; set; }
}
```
⸻

## CLASS LEVEL ATTRIBUTES

- Applied on Class.


### [Table]

**Purpose:**
- Specify table name.
```cs
[Table("Employees")]
public class Employee
{
}
```
**Result:**
- Employees Table

---

### [Index]

**Purpose:**
- Create database index.
```cs
[Index(nameof(Email))]
public class Employee
{
}
```
**Result:**
- Faster Searching

---

### [Index(IsUnique = true)]

**Purpose:**

- Create unique index.
```cs
[Index(nameof(Email), IsUnique = true)]
public class Employee
{
}
```
**Result:**
- Duplicate Emails Not Allowed

---

### [PrimaryKey]

**Purpose:**

- Composite primary key.
```cs
[PrimaryKey(nameof(Id), nameof(Code))]
public class Product
{
}
```
**Result:**
- (Id + Code) = Primary Key

---

### [Owned]

**Purpose:**
- Owned Entity Type.

```cs
[Owned]
public class Address
{
}
```
**Result:**
- Embedded Entity

------------------

## PROPERTY LEVEL ATTRIBUTES
- Applied on Properties.


### [Key]

**Purpose:**
- Primary Key.

```cs
[Key]
public int EmployeeId { get; set; }
```

**Result:**
- EmployeeId INT PRIMARY KEY

---

### [Required]

**Purpose:**
- Cannot be NULL.

```cs
[Required]
public string Name { get; set; }
```

**Result:**
- Name NOT NULL


### [Required(AllowEmptyStrings = false)]

**Purpose:**
- Cannot be NULL or Empty.

```cs
[Required(AllowEmptyStrings = false)]
public string Name { get; set; }
```

### [MaxLength]

**Purpose:**
- Maximum length.

```cs
[MaxLength(100)]
public string Name { get; set; }
```

**Result:**
- NVARCHAR(100)


### [MinLength]

**Purpose:**
- Minimum length.

```cs
[MinLength(3)]
public string Name { get; set; }
```

### [StringLength]

**Purpose:**
- Minimum and Maximum length.

```cs
[StringLength(100, MinimumLength = 3)]
public string Name { get; set; }
```

### [Length]

**Purpose:**
- Minimum and Maximum length.

```cs
[Length(3,50)]
public string Name { get; set; }
```

### [Column]

**Purpose:**
- Custom column name.

```cs
[Column("EmployeeName")]
public string Name { get; set; }
```
**Result:**
- EmployeeName


### [Column(TypeName)]

**Purpose:**
- Specify exact SQL datatype.

```cs
[Column(TypeName = "varchar(50)")]
public string Name { get; set; }
```
**Result:**
- VARCHAR(50)

#### Common SQL Types:
```cs
[Column(TypeName="varchar(50)")]
[Column(TypeName="nvarchar(100)")]
[Column(TypeName="char(10)")]
[Column(TypeName="decimal(18,2)")]
[Column(TypeName="date")]
[Column(TypeName="datetime")]
```
⸻

### [NotMapped]

**Purpose:**
- Ignore property.

```cs
[NotMapped]
public int Age { get; set; }
```

**Result:**
- No Column Created


### [ForeignKey]

**Purpose:**

- Define foreign key.

```cs
public int DepartmentId { get; set; }
[ForeignKey("DepartmentId")]
public Department Department
{
    get;
    set;
}
```

**Result:**
- Connects Two Tables

Rule: How to use: / auto-generated
- Data must be saved before
- If anthing mistake like - use trancsaction, rollback


### [InverseProperty]

**Purpose:**
- Configure multiple relationships.

```cs
[InverseProperty("Manager")]
public ICollection<Employee>
Employees
{
    get;
    set;
}
```


### [DatabaseGenerated]

**Purpose:**

- Auto generated values.
```cs
[DatabaseGenerated(DatabaseGeneratedOption.Identity)]
public int Id { get; set; }
```
**Options:**

- Identity
- Computed
- None


### [Range]

**Purpose:**
- Minimum and Maximum value validation.

```cs
[Range(1,100)]
public int Age { get; set; }
```

### [Precision]

**Purpose:**
- Decimal precision.

```cs
[Precision(18,2)]
public decimal Salary { get; set; }
```

**Result:**
- DECIMAL(18,2)


### [Unicode]

**Purpose:**
- Enable or disable Unicode.
```cs
[Unicode(false)]
public string Code { get; set; }
```
**Result:**
- VARCHAR instead of NVARCHAR

### [EmailAddress]

**Purpose:**
- Validate email.

```cs
[EmailAddress]
public string Email { get; set; }
```
**Example:**
- abc@gmail.com

### [Phone]

**Purpose:**
- Validate phone number.

```cs
[Phone]
public string Mobile { get; set; }
```
⸻

### [Url]

**Purpose:**
- Validate URL.

```cs
[Url]
public string Website { get; set; }
```

### [CreditCard]

**Purpose:**
- Validate card number.

```cs
[CreditCard]
public string CardNumber { get; set; }
```

### [RegularExpression]

**Purpose:**
- Custom validation pattern.

```cs
[RegularExpression(@"^[A-Za-z]+$")]
public string Name { get; set; }
```

### [Compare]

**Purpose:**
- Compare two properties.

```cs
[Compare("Password")]
public string ConfirmPassword
{
    get;
    set;
}
```

### [DataType]

**Purpose:**
- Specify datatype.

```cs
[DataType(DataType.Date)]
public DateTime DOB { get; set; }
```

**Common Types:**
- Date
- Time
- Currency
- Password
- EmailAddress
- PhoneNumber


### [Display]

**Purpose:**
- Display friendly name.

```cs
[Display(Name = "Employee Name")]
public string Name { get; set; }
```

### [DisplayFormat]

**Purpose:**
- Format display value.

```cs
[DisplayFormat(DataFormatString = "{0:dd/MM/yyyy}")]
public DateTime DOB
{
    get;
    set;
}
```

### [Timestamp]

**Purpose:**
- Concurrency handling.

```cs
[Timestamp]
public byte[] RowVersion
{
    get;
    set;
}
```

### [ConcurrencyCheck]

**Purpose:**
- Detect concurrent updates.

```cs
[ConcurrencyCheck]
public string Name { get; set; }
```

### [PersonalData]

**Purpose:**
- ASP.NET Identity personal data.

```cs
[PersonalData]
public string PhoneNumber
{
    get;
    set;
}
```

### [ProtectedPersonalData]

**Purpose:**
- Protected personal data.

```cs
[ProtectedPersonalData]
public string AadhaarNumber
{
    get;
    set;
}
```

**Classification:**
- Database Configuration

[Key]
[Table]
[Column]
[Column(TypeName)]
[ForeignKey]
[DatabaseGenerated]
[NotMapped]
[Precision]
[Unicode]
[Index]
[PrimaryKey]
[Owned]
[InverseProperty]

⸻

Validation

[Required]
[Required(AllowEmptyStrings = false)]
[Range]
[StringLength]
[Length]
[MinLength]
[MaxLength]
[EmailAddress]
[Phone]
[Url]
[CreditCard]
[RegularExpression]
[Compare]

⸻

UI / Display

[Display]
[DisplayFormat]
[DataType]

⸻

Concurrency

[Timestamp]
[ConcurrencyCheck]

⸻

ASP.NET Identity

[PersonalData]
[ProtectedPersonalData]