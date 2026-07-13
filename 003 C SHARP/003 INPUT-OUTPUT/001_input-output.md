# Input & Output in C#

---

# Input & Output

Input and Output are used to interact with the user.

- **Output** → Display data on the screen.
- **Input** → Read data entered by the user.

---

# Console.WriteLine()

`Console.WriteLine()` is used to print text or values on the console.

### Syntax

```csharp
Console.WriteLine(value);
```

### Example

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.WriteLine("Hello World");
        Console.WriteLine(100);
        Console.WriteLine(3.14);
    }
}
```

**Output**

```text
Hello World
100
3.14
```

---

# Console.ReadLine()

`Console.ReadLine()` is used to read a line of input from the keyboard.

It always returns a **string**.

### Example

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Enter your name: ");

        string name = Console.ReadLine();

        Console.WriteLine("Welcome " + name);
    }
}
```

**Output**

```text
Enter your name: John
Welcome John
```

### Reading an Integer

```csharp
using System;

class Program
{
    static void Main()
    {
        Console.Write("Enter Age: ");

        int age = int.Parse(Console.ReadLine());

        Console.WriteLine(age);
    }
}
```

---

# String Formatting

String formatting uses placeholders (`{0}`, `{1}`, etc.) to insert values into a string.

### Syntax

```csharp
Console.WriteLine("Text {0}", value);
```

### Example

```csharp
using System;

class Program
{
    static void Main()
    {
        string name = "John";
        int age = 22;

        Console.WriteLine("Name: {0}", name);
        Console.WriteLine("Age: {0}", age);
        Console.WriteLine("{0} is {1} years old.", name, age);
    }
}
```

**Output**

```text
Name: John
Age: 22
John is 22 years old.
```

---

# String Interpolation

String interpolation uses the `$` symbol to insert variables directly into a string.

### Syntax

```csharp
$"Text {variable}"
```

### Example

```csharp
using System;

class Program
{
    static void Main()
    {
        string name = "John";
        int age = 22;

        Console.WriteLine($"Name: {name}");
        Console.WriteLine($"Age: {age}");
        Console.WriteLine($"{name} is {age} years old.");
    }
}
```

**Output**

```text
Name: John
Age: 22
John is 22 years old.
```