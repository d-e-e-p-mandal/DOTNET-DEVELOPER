
## ADVANCED

## API BEHAVIOR / RESPONSE (IMPORTANT)
```cs
[Produces("application/json")]  
// response type
[Consumes("application/json")]  
// request type
[ProducesResponseType(200)]  
// expected response code
[ProducesResponseType(404)]  
// document API response
```

## Extra:

```cs
[Timestamp]          // concurrency control

[ConcurrencyCheck]   // prevent overwrite

[BindNever]          // ignore in request binding

[BindRequired]       // must be present in request
```



#### EXTRA VALIDATION ATTRIBUTES (IMPORTANT)
```cs
[CreditCard]          // validate credit card number
[EnumDataType(typeof(MyEnum))]  
// restrict value to enum
[FileExtensions(Extensions = "jpg,png")]  
// validate file type
[Length(min, max)]  
// .NET 8+ → combine MinLength + MaxLength
```


#### EF CORE ADVANCED (IMPORTANT)
```cs
[Index(nameof(Name))]  
// create index (performance)
[Precision(10,2)]  
// decimal precision (e.g., salary)
[Owned]  
// owned entity (value object)
```
