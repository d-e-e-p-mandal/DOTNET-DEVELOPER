
### 3. VALIDATION (REQUEST SIDE)

- Used when client sends data (POST/PUT)
```cs
[Phone]                        // phone validation

[Url]                          // URL validation

[Compare("Password")]          // compare fields

[RegularExpression("pattern")] // custom validation

[DataType(DataType.Password)]  // UI hint (password/date)
```

