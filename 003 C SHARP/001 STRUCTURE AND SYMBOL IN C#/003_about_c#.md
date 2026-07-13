# C# Basics

# What is C#?

**C# (C-Sharp)** is a modern, object-oriented programming language developed by Microsoft. It is used to build many types of applications such as:

- Console Applications
- Windows Applications
- Web Applications
- Mobile Applications
- Desktop Applications
- Cloud Applications
- Games using Unity

C# runs on the **.NET Platform**, which provides libraries and runtime support.

### Example

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello, World!");
    }
}
```

Output

```
Hello, World!
```

---

# History of C#

- Developed by **Microsoft**.
- Designed by **Anders Hejlsberg**.
- Introduced in **2000**.
- Released with **.NET Framework 1.0** in **2002**.
- Standardized by ECMA and ISO.
- Continuously updated with new versions.

| Version | Features |
|----------|----------|
| C# 1.0 | Basic Object-Oriented Programming |
| C# 2.0 | Generics |
| C# 3.0 | LINQ |
| C# 4.0 | Dynamic Type |
| C# 5.0 | Async and Await |
| C# 6.0 | Expression-bodied Members |
| C# 7.x | Tuples, Pattern Matching |
| C# 8.0 | Nullable Reference Types |
| C# 9.0 | Records |
| C# 10 | Global Using |
| C# 11 | Raw String Literals |
| C# 12 | Primary Constructors and more |

---

# Features of C#

C# provides many powerful features.

## 1. Simple

Easy to learn and easy to read.

```csharp
int age = 20;
```

---

## 2. Object-Oriented

Supports:

- Class
- Object
- Inheritance
- Polymorphism
- Encapsulation
- Abstraction

```csharp
class Student
{
    public string Name;
}
```

---

## 3. Type Safe

Variables must have a proper data type.

```csharp
int number = 10;

// Error
// number = "Hello";
```

---

## 4. Platform Independent

Applications run on multiple operating systems using .NET.

- Windows
- Linux
- macOS

---

## 5. Automatic Memory Management

Memory is managed automatically using the Garbage Collector (GC).

```csharp
Student s = new Student();
```

---

## 6. Rich Library Support

Provides thousands of built-in classes.

```csharp
using System;
using System.IO;
using System.Collections.Generic;
```

---

## 7. Exception Handling

```csharp
try
{
    int x = 10;
}
catch(Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

---

## 8. Multithreading

Supports running multiple tasks simultaneously.

```csharp
using System.Threading;
```

---

## 9. Secure

Provides strong type checking and managed code.

---

## 10. Modern Language

Supports:

- Generics
- LINQ
- Async Programming
- Lambda Expressions
- Pattern Matching

---

# Structure of a C# Program

Basic structure of a C# program:

```csharp
using System;

namespace Demo
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World");
        }
    }
}
```

### Structure Explanation

| Part | Description |
|------|-------------|
| using | Imports namespaces |
| namespace | Groups related classes |
| class | Defines a class |
| Main() | Program entry point |
| Statements | Program instructions |

---

# Main() Method

The **Main()** method is the entry point of every C# console application.

Execution always starts from `Main()`.

### Syntax

```csharp
static void Main()
{

}
```

or

```csharp
static void Main(string[] args)
{

}
```

### Example

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Program Started");
    }
}
```

Output

```
Program Started
```

### Command Line Arguments

```csharp
using System;

class Program
{
    static void Main(string[] args)
    {
        Console.WriteLine("Arguments:");

        foreach(string item in args)
        {
            Console.WriteLine(item);
        }
    }
}
```

---

# Comments

Comments are used to explain code and are ignored by the compiler.

## Single-Line Comment

```csharp
// This is a single-line comment

Console.WriteLine("Hello");
```

---

## Multi-Line Comment

```csharp
/*
This is
a multi-line
comment.
*/

Console.WriteLine("Hello");
```

---

## XML Documentation Comment

```csharp
/// <summary>
/// Adds two numbers.
/// </summary>
```

Used to generate API documentation.

---

# Statements

A **statement** is an instruction that tells the computer what to do.

Every statement usually ends with a semicolon (`;`).

## Variable Declaration

```csharp
int age = 20;
```

---

## Assignment Statement

```csharp
age = 25;
```

---

## Method Call

```csharp
Console.WriteLine(age);
```

---

## Conditional Statement

```csharp
if(age >= 18)
{
    Console.WriteLine("Adult");
}
```

---

## Loop Statement

```csharp
for(int i = 1; i <= 5; i++)
{
    Console.WriteLine(i);
}
```

---

## Return Statement

```csharp
return;
```

---

# Namespaces

A **namespace** is used to organize related classes, interfaces, enums, and other types.

It helps avoid naming conflicts.

## Syntax

```csharp
namespace MyApplication
{

}
```

---

## Example

```csharp
using System;

namespace MyApplication
{
    class Program
    {
        static void Main()
        {
            Console.WriteLine("Welcome");
        }
    }
}
```

---

## Creating Multiple Namespaces

```csharp
namespace College
{
    class Student
    {

    }
}

namespace Office
{
    class Employee
    {

    }
}
```

---

## Using a Namespace

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello");
    }
}
```

---

## Fully Qualified Namespace

```csharp
System.Console.WriteLine("Hello");
```

---

## Advantages of Namespaces

- Organizes code.
- Prevents naming conflicts.
- Improves readability.
- Makes large projects easier to manage.
- Groups related classes together.

---