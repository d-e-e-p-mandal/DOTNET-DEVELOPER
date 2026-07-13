### 2. PROPERTY LEVEL (CORE VALIDATION)
```cs
[Key]                  // primary key

[Required]             // cannot be null (request validation)

[Range(1000, 100000)]  // numeric validation

[StringLength(50)]     // string length

[MaxLength(100)]       // max length

[MinLength(3)]         // min length

[EmailAddress]         // email format
```