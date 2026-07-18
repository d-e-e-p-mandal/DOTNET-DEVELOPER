# C# Operators (`?`, `??`, `?.`, `!`, `??=`, etc.) Complete Notes

# Introduction

C# provides several operators using the `?` and `!` symbols. These operators help with:

- Null handling
- Nullable value types
- Null-safe access
- Pattern matching
- Conditional expressions
- Nullable reference types

---

# 1. Ternary Conditional Operator (`?:`)

Used as a short form of if-else.

## Syntax

```csharp
condition ? valueIfTrue : valueIfFalse;
```

## Example

```csharp
int age = 20;

string result = age >= 18 ? "Adult" : "Minor";

Console.WriteLine(result);
```

Output

```
Adult
```

Equivalent

```csharp
string result;

if(age >= 18)
    result = "Adult";
else
    result = "Minor";
```

When to use

- Return one of two values
- Short if-else

---

# 2. Nullable Value Type (`?`)

Allows value types to contain null.

Normally

```csharp
int number = null;
```

Error

Because int cannot be null.

Use

```csharp
int? number = null;
```

Example

```csharp
int? age = null;

Console.WriteLine(age);
```

Output

```
null
```

Another example

```csharp
int? salary = 25000;
```

Without nullable

```
int
```

Possible values

```
0
1
500
```

With nullable

```
null
0
1
500
```

Equivalent

```csharp
Nullable<int> number = null;
```

---

# 3. Null Conditional Operator (`?.`)

Safely access properties or methods.

Without

```csharp
employee.Name
```

If employee is null

```
NullReferenceException
```

Using

```csharp
employee?.Name
```

If employee is null

Result

```
null
```

Example

```csharp
Employee emp = null;

Console.WriteLine(emp?.Name);
```

No exception.

---

Method Example

```csharp
emp?.Print();
```

If emp is null

Nothing happens.

---

Collection Example

```csharp
Console.WriteLine(list?.Count);
```

---

Chain Example

```csharp
employee?.Department?.Manager?.Name
```

Every object checked automatically.

---

# 4. Null Coalescing Operator (`??`)

Provides default value when left side is null.

Syntax

```csharp
value ?? defaultValue
```

Example

```csharp
string name = null;

string result = name ?? "Guest";
```

Output

```
Guest
```

Another

```csharp
string name = "Deep";

string result = name ?? "Guest";
```

Output

```
Deep
```

Equivalent

```csharp
if(name == null)
    result = "Guest";
else
    result = name;
```

---

# 5. Null Coalescing Assignment (`??=`)

Assign only if variable is null.

Example

```csharp
string name = null;

name ??= "Guest";
```

Result

```
Guest
```

If

```csharp
string name = "Deep";

name ??= "Guest";
```

Result

```
Deep
```

No change.

Equivalent

```csharp
if(name == null)
{
    name = "Guest";
}
```

---

# 6. Null Forgiving Operator (`!`)

Tells compiler

> "I know this isn't null."

Example

```csharp
string? name = GetName();

Console.WriteLine(name!.Length);
```

Without

Compiler warning

```
Possible null reference.
```

With

```csharp
name!
```

Warning removed.

Important

This DOES NOT check null.

If actually null

```
NullReferenceException
```

It only removes compiler warning.

---

# 7. Null Conditional Index (`?[]`)

Safely access array/list index.

Example

```csharp
List<string> names = null;

Console.WriteLine(names?[0]);
```

Output

```
null
```

Without

```csharp
names[0]
```

Exception

```
NullReferenceException
```

---

# 8. Nullable Reference Type (`string?`)

Available from C# 8.

Example

```csharp
string? name = null;
```

Compiler knows

```
This variable may be null.
```

Without

```csharp
string name;
```

Compiler expects

```
Never null
```

---

Example

```csharp
string? firstName = null;
```

---

# 9. Pattern Matching (`is` with `?`)

Example

```csharp
if(obj is string text)
{
    Console.WriteLine(text);
}
```

Another

```csharp
if(number is int value)
{
    Console.WriteLine(value);
}
```

---

# 10. Nullable Boolean (`bool?`)

Three states

```csharp
bool? result;
```

Possible values

```
true
false
null
```

Example

```csharp
bool? approved = null;
```

Useful

- Database
- Unknown state
- Optional values

---

# 11. Delegate Safe Invocation (`?.Invoke()`)

Without

```csharp
if(MyEvent != null)
{
    MyEvent();
}
```

Using

```csharp
MyEvent?.Invoke();
```

Cleaner and thread-safe.

---

# 12. Combining `?.` and `??`

Very common.

Example

```csharp
string result = employee?.Name ?? "Unknown";
```

Meaning

If employee exists

```
Return employee.Name
```

Otherwise

```
Unknown
```

---

Example

```csharp
Console.WriteLine(employee?.Department?.Manager?.Name ?? "No Manager");
```

---

# 13. Combining `??=` and `?.`

Example

```csharp
employee ??= new Employee();

employee?.Print();
```

---

# 14. Using Nullable with LINQ

Example

```csharp
Employee? emp =
    employees.FirstOrDefault(x => x.Id == 1);

Console.WriteLine(emp?.Name ?? "Not Found");
```

Very common in ASP.NET Core.

---

# 15. Using Nullable with XML

```csharp
var name = doc.Root?
              .Element("Employee")?
              .Element("Name")?
              .Value;
```

No exception if node missing.

---

# 16. Using Nullable with Database

```csharp
string result =
reader["Name"]?.ToString() ?? "";
```

---

# 17. Using Nullable with API

```csharp
Console.WriteLine(response?.User?.Email ?? "No Email");
```

---

# Quick Comparison

| Operator | Name | Purpose |
|-----------|------|---------|
| `?:` | Ternary | Short if-else |
| `?` | Nullable Value Type | Allow null in value types |
| `string?` | Nullable Reference | Reference may be null |
| `?.` | Null Conditional | Safe property/method access |
| `?[]` | Null Conditional Index | Safe array/list indexing |
| `??` | Null Coalescing | Default value if null |
| `??=` | Null Coalescing Assignment | Assign only when null |
| `!` | Null Forgiving | Suppress nullable warnings |
| `?.Invoke()` | Safe Delegate Invocation | Invoke delegate/event only if not null |

---

# Real ASP.NET Core Examples

## Example 1

```csharp
Employee? emp = repository.GetById(id);

return emp?.Name ?? "Employee Not Found";
```

---

## Example 2

```csharp
model ??= new EmployeeModel();
```

---

## Example 3

```csharp
ViewBag.Name = user?.Name;
```

---

## Example 4

```csharp
_logger?.LogInformation("Application Started");
```

---

## Example 5

```csharp
var city = customer?.Address?.City ?? "Unknown";
```

---

# Easy Memory Trick

| Symbol | Remember As |
|---------|-------------|
| `?` | Can be null |
| `?.` | If not null, continue |
| `??` | If null, use another value |
| `??=` | Assign only if null |
| `!` | Trust me, it's not null |
| `?:` | Short if-else |
| `?[]` | Safe index access |
| `?.Invoke()` | Call only if not null |

---

# Interview Questions

### Q1. Difference between `?.` and `??`

`?.` safely accesses a member and returns `null` if the object is null.

```csharp
employee?.Name
```

`??` provides a fallback value if the left side is null.

```csharp
employee?.Name ?? "Unknown"
```

---

### Q2. Difference between `??` and `??=`

`??` returns a default value without changing the variable.

```csharp
string result = name ?? "Guest";
```

`??=` assigns the default value to the variable if it is null.

```csharp
name ??= "Guest";
```

---

### Q3. Difference between `!` and `?.`

`!` only suppresses the compiler's nullable warning; it does not prevent a `NullReferenceException`.

```csharp
name!.Length
```

`?.` safely checks for null before accessing a member.

```csharp
name?.Length
```

---

### Q4. Why use `int?` instead of `int`?

`int` cannot hold `null`, while `int?` can.

```csharp
int? age = null;
```

Useful for optional values or database fields that allow `NULL`.

---

### Q5. Which operators are used most in ASP.NET Core?

- `?.`
- `??`
- `??=`
- `string?`
- `int?`
- `?.Invoke()`

These are commonly used when working with APIs, Entity Framework Core, LINQ, XML, JSON, and nullable reference types.