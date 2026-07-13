

### 4. DATABASE / SCHEMA (EF CORE)
```cs
using System.ComponentModel.DataAnnotations.Schema;
```

```cs
[Column("EmpName")]    // column name in DB

[NotMapped]            // not stored in DB

[ForeignKey("DeptId")] // foreign key

[DatabaseGenerated(DatabaseGeneratedOption.Identity)] // auto increment
```
