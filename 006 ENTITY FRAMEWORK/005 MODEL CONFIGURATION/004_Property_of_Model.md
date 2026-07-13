# Model Creation :

```cs
public string Name {get; set; }
```

**Internally:**
- The compiler creates a hidden field automatically:
```cs
private string _name;

public string Name
{
    get { return _name; }
    set { _name = value; }
}
```


-----

## 1. Auto Property
```cs
public string Name { get; set; }
```


## 2. Property with Default Value
```cs
public string Name { get; set; } = "";
public int Age { get; set; } = 18;
```


## 3. Nullable Property
```cs
public string? Name { get; set; }
public int? Age { get; set; }
```


## 4. Non-Nullable with Null Forgiving Operator
```cs
public string Name { get; set; } = null!;
```
Used when value will be assigned later.



## 5. Required Property (C# 11)
```
public required string Name { get; set; }
```
- Must be initialized during object creation.



## 6. Required + Nullable
```cs
public required string? Name { get; set; }
```


## 7. Required + Null Forgiving
```cs
public required string Name { get; set; } = null!;
```

## 8. Read Only Property
```cs
public string Name { get; }
```
or
```cs
public string Name { get; init; }
```


## 9. Init Only Property
```cs
public string Name { get; init; }
```
Can only be set during object creation.

Example:
```cs
var user = new User
{
    Name = "Deep"
};
```


## 10. Private Setter
```cs
public string Name { get; private set; }
```
- Read from outside, modify only inside class.



## 11. Protected Setter
```cs
public string Name { get; protected set; }
```


## 12. Internal Setter
```cs
public string Name { get; internal set; }
```


## 13. Private Getter
```cs
public string Name { private get; set; }
```
- Rarely used.



## 14. Expression Bodied Read Only Property
```cs
public string FullName => FirstName + " " + LastName;
```


## 15. Computed Property
```cs
public int Age => DateTime.Now.Year - BirthYear;
```


## 16. Property with Validation
```cs
private int _age;
public int Age
{
    get { return _age; }
    set
    {
        if (value >= 0)
            _age = value;
    }
}
```


## 17. Static Property
```cs
public static string CompanyName { get; set; }
```


## 18. Virtual Property
```cs
public virtual string Name { get; set; }
```


## 19. Override Property
```cs
public override string Name { get; set; }
```


## 20. Abstract Property
```cs
public abstract string Name { get; set; }
```


## 21. EF Core Navigation Property
```cs
public virtual Department Department { get; set; } = null!;
public virtual ICollection<Employee> Employees { get; set; } = new List<Employee>();
```


## 22. Record Init Property
```cs
public record User
{
    public string Name { get; init; } = "";
}
```