# Methods (Functions) in C#

---

# What is a Method?

A **method** (also called a **function**) is a block of code that performs a specific task.

Methods help make programs:
- Reusable
- Easy to read
- Easy to maintain

A method is executed only when it is called.

---

# Method Declaration

A method declaration defines the method name, return type, and parameters.

### Syntax

```csharp
returnType MethodName(parameters)
{
    // Code
}
```

### Example

```csharp
using System;

class Program
{
    static void Display()
    {
        Console.WriteLine("Hello C#");
    }

    static void Main()
    {
        Display();
    }
}
```

---

# Parameters

Parameters are values passed to a method.

### Syntax

```csharp
returnType MethodName(dataType parameter)
{
    // Code
}
```

### Example

```csharp
using System;

class Program
{
    static void Greet(string name)
    {
        Console.WriteLine("Hello " + name);
    }

    static void Main()
    {
        Greet("John");
    }
}
```

---

# Return Types

A method can return a value using the `return` keyword.

### Example

```csharp
using System;

class Program
{
    static int Add(int a, int b)
    {
        return a + b;
    }

    static void Main()
    {
        int result = Add(10, 20);

        Console.WriteLine(result);
    }
}
```

---

# Method Overloading

Method overloading means creating multiple methods with the **same name** but **different parameters**.

### Example

```csharp
using System;

class Program
{
    static int Add(int a, int b)
    {
        return a + b;
    }

    static double Add(double a, double b)
    {
        return a + b;
    }

    static void Main()
    {
        Console.WriteLine(Add(10, 20));
        Console.WriteLine(Add(2.5, 3.5));
    }
}
```

---

# Named Parameters

Named parameters allow passing arguments using the parameter names.

### Example

```csharp
using System;

class Program
{
    static void Student(string name, int age)
    {
        Console.WriteLine(name);
        Console.WriteLine(age);
    }

    static void Main()
    {
        Student(age: 21, name: "John");
    }
}
```

---

# Optional Parameters

Optional parameters have default values. If no value is passed, the default value is used.

### Example

```csharp
using System;

class Program
{
    static void Greet(string name = "Guest")
    {
        Console.WriteLine("Hello " + name);
    }

    static void Main()
    {
        Greet();
        Greet("John");
    }
}
```

---

# ref Keyword

The `ref` keyword passes a variable **by reference**.

The variable **must be initialized** before passing it.

### Example

```csharp
using System;

class Program
{
    static void Increment(ref int number)
    {
        number++;
    }

    static void Main()
    {
        int value = 10;

        Increment(ref value);

        Console.WriteLine(value);
    }
}
```

---

# out Keyword

The `out` keyword passes a variable by reference and is used to return values from a method.

The variable **does not need to be initialized** before passing.

### Example

```csharp
using System;

class Program
{
    static void GetValues(out int a, out int b)
    {
        a = 10;
        b = 20;
    }

    static void Main()
    {
        int x, y;

        GetValues(out x, out y);

        Console.WriteLine(x);
        Console.WriteLine(y);
    }
}
```

---

# params Keyword

The `params` keyword allows a method to accept a variable number of arguments.

### Example

```csharp
using System;

class Program
{
    static int Sum(params int[] numbers)
    {
        int total = 0;

        foreach (int num in numbers)
        {
            total += num;
        }

        return total;
    }

    static void Main()
    {
        Console.WriteLine(Sum(10, 20));
        Console.WriteLine(Sum(1, 2, 3, 4, 5));
    }
}
```

---

# Difference Between ref and out

| ref | out |
|------|------|
| Variable must be initialized | Variable need not be initialized |
| Used to modify an existing value | Used to return values from a method |
| Must be assigned before passing | Must be assigned inside the method |

---
