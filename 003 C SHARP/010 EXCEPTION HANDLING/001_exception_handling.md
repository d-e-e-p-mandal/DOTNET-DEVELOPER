# Exception Handling in C#

- An **exception** is an error that occurs while a program is running.
- **Exception Handling** allows the program to handle errors gracefully without crashing.

- C# provides the following keywords for exception handling:
    - `try`
    - `catch`
    - `finally`
    - `throw`


## try Block
The `try` block contains code that may generate an exception.

**Syntax:**
```csharp
try
{
    // Code that may cause an exception
}
```

**Example:**
```csharp
try
{
    int result = 10 / 0;
}
catch
{
    Console.WriteLine("Exception occurred.");
}
```

---

## catch Block
The `catch` block handles the exception generated in the `try` block.

**Syntax:**
```csharp
try
{
    // Code
}
catch(Exception ex)
{
    // Handle exception
}
```

**Example:**
```csharp
using System;

class Program
{
    static void Main()
    {
        try
        {
            int a = 10;
            int b = 0;

            Console.WriteLine(a / b);
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

---

## finally Block

The `finally` block always executes whether an exception occurs or not.

It is commonly used to release resources such as files or database connections.

### Syntax

```csharp
try
{
    // Code
}
catch
{
    // Handle exception
}
finally
{
    // Always executes
}
```

### Example

```csharp
try
{
    Console.WriteLine("Inside Try");
}
catch
{
    Console.WriteLine("Inside Catch");
}
finally
{
    Console.WriteLine("Inside Finally");
}
```

---

## throw Keyword
The `throw` keyword is used to manually create and throw an exception.

**Example:**
```csharp
using System;

class Program
{
    static void CheckAge(int age)
    {
        if (age < 18)
        {
            throw new Exception("Age must be 18 or above.");
        }

        Console.WriteLine("Eligible");
    }

    static void Main()
    {
        try
        {
            CheckAge(16);
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

---

### Custom Exceptions
- A custom exception is a user-defined exception class.
- It is created by inheriting from the `Exception` class.

**Example:**

```csharp
using System;

class AgeException : Exception
{
    public AgeException(string message) : base(message)
    {

    }
}

class Program
{
    static void Main()
    {
        try
        {
            throw new AgeException("Invalid Age");
        }
        catch (AgeException ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

---

### Multiple Catch Blocks
- A `try` block can have multiple `catch` blocks to handle different types of exceptions.

**Example:**

```csharp
using System;

class Program
{
    static void Main()
    {
        try
        {
            int[] numbers = {1, 2, 3};

            Console.WriteLine(numbers[5]);
        }
        catch (IndexOutOfRangeException)
        {
            Console.WriteLine("Index Out of Range.");
        }
        catch (Exception)
        {
            Console.WriteLine("General Exception.");
        }
    }
}
```

---

# Exception Propagation

Exception propagation means an exception is passed from one method to another until it is handled.

### Example

```csharp
using System;

class Program
{
    static void Method2()
    {
        int a = 10;
        int b = 0;

        Console.WriteLine(a / b);
    }

    static void Method1()
    {
        Method2();
    }

    static void Main()
    {
        try
        {
            Method1();
        }
        catch (Exception ex)
        {
            Console.WriteLine(ex.Message);
        }
    }
}
```

In this example:

- `Method2()` generates the exception.
- The exception moves to `Method1()`.
- Finally, it is handled in `Main()`.

This process is called **Exception Propagation**.

---

# Common Exception Classes

| Exception | Description |
|-----------|-------------|
| `Exception` | Base class for all exceptions |
| `DivideByZeroException` | Division by zero |
| `NullReferenceException` | Accessing a null object |
| `IndexOutOfRangeException` | Invalid array index |
| `FormatException` | Invalid input format |
| `InvalidOperationException` | Invalid operation |
| `OverflowException` | Arithmetic overflow |
| `FileNotFoundException` | File not found |
---