# Built-in Delegates in C#
- C# provides predefined delegates that eliminate the need to declare your own delegate.
- The most commonly used built-in delegates are:

- `Action`
- `Func`
- `Predicate`

### Namespace
```csharp
using System;
```

### Difference Between Action, Func and Predicate
| Delegate | Parameters | Return Type | Purpose |
|----------|------------|-------------|---------|
| `Action` | 0 to 16 | `void` | Performs an action |
| `Func` | 0 to 16 | Any Type | Returns a value |
| `Predicate<T>` | 1 | `bool` | Tests a condition |


## Action Delegate
- `Action` is a built-in delegate that **does not return any value** (`void`).
- It can take **0 to 16 parameters**.

### Syntax
```csharp
Action actionName;
```

or:

```csharp
Action<T1, T2, ...> actionName;
```

### Example: No Parameter
```csharp
using System;
class Program
{
    static void Main()
    {
        Action message = () =>
        {
            Console.WriteLine("Hello C#");
        };

        message();
    }
}
```

**Output**

```text
Hello C#
```

### Example: With Parameter
```csharp
using System;
class Program
{
    static void Main()
    {
        Action<string> greet = (name) =>
        {
            Console.WriteLine("Hello " + name);
        };

        greet("John");
    }
}
```

**Output**

```text
Hello John
```

---

## Func Delegate
- `Func` is a built-in delegate that **returns a value**.
- The **last type parameter** is always the return type.
- It can have **0 to 16 input parameters**.

### Syntax

```csharp
Func<ReturnType> functionName;
```

or:

```csharp
Func<T1, T2, ReturnType> functionName;
```


### Example

```csharp
using System;
class Program
{
    static void Main()
    {
        Func<int, int, int> add = (a, b) =>
        {
            return a + b;
        };

        Console.WriteLine(add(10, 20));
    }
}
```

**Output**

```text
30
```

---

## Predicate Delegate
- `Predicate<T>` is a built-in delegate that **returns only a boolean value** (`true` or `false`).
- It accepts **one input parameter**.

### Syntax
```csharp
Predicate<T> predicateName;
```


### Example

```csharp
using System;
class Program
{
    static void Main()
    {
        Predicate<int> isEven = (number) =>
        {
            return number % 2 == 0;
        };

        Console.WriteLine(isEven(10));
        Console.WriteLine(isEven(7));
    }
}
```

**Output**

```text
True
False
```

---



---

# When to Use

### Use `Action`

- Printing output
- Logging
- Executing tasks
- No return value

### Use `Func`

- Mathematical operations
- Calculations
- Returning values
- Data processing

### Use `Predicate`

- Searching
- Filtering collections
- Validating data
- Checking conditions

--