# Recursion in C#

---

# What is Recursion?

**Recursion** is a technique in which a method calls itself to solve a problem.

A recursive method must have:

- **Base Case** → Stops the recursion.
- **Recursive Call** → Calls the same method again.

Without a base case, the recursion will continue forever and cause a **StackOverflowException**.

---

# Recursive Function

A recursive function is a function that calls itself.

### Syntax

```csharp
returnType FunctionName(parameters)
{
    if(baseCondition)
    {
        return value;
    }

    return FunctionName(smallerProblem);
}
```

### Example

```csharp
using System;

class Program
{
    static void Print(int n)
    {
        if (n == 0)
            return;

        Console.WriteLine(n);

        Print(n - 1);
    }

    static void Main()
    {
        Print(5);
    }
}
```

**Output**

```text
5
4
3
2
1
```

---

# Factorial Using Recursion

The factorial of a number is:

```text
5! = 5 × 4 × 3 × 2 × 1 = 120
```

### Example

```csharp
using System;

class Program
{
    static int Factorial(int n)
    {
        if (n == 0 || n == 1)
            return 1;

        return n * Factorial(n - 1);
    }

    static void Main()
    {
        Console.WriteLine(Factorial(5));
    }
}
```

**Output**

```text
120
```

---

# Fibonacci Using Recursion

The Fibonacci sequence is:

```text
0 1 1 2 3 5 8 13 ...
```

Each number is the sum of the previous two numbers.

### Example

```csharp
using System;

class Program
{
    static int Fibonacci(int n)
    {
        if (n == 0)
            return 0;

        if (n == 1)
            return 1;

        return Fibonacci(n - 1) + Fibonacci(n - 2);
    }

    static void Main()
    {
        Console.WriteLine(Fibonacci(6));
    }
}
```

**Output**

```text
8
```

---

# Recursive Traversal

Recursive traversal means visiting elements one by one using recursion.

### Example (Array Traversal)

```csharp
using System;

class Program
{
    static void PrintArray(int[] arr, int index)
    {
        if (index == arr.Length)
            return;

        Console.WriteLine(arr[index]);

        PrintArray(arr, index + 1);
    }

    static void Main()
    {
        int[] numbers = {10, 20, 30, 40};

        PrintArray(numbers, 0);
    }
}
```

**Output**

```text
10
20
30
40
```

---

# Advantages of Recursion

- Simple and easy to understand.
- Reduces code for complex problems.
- Useful for trees and graphs.
- Useful for divide-and-conquer algorithms.

---

# Disadvantages of Recursion

- Uses more memory due to function calls.
- Can be slower than loops.
- Missing a base case causes infinite recursion.
- Deep recursion may cause a `StackOverflowException`.

---

# Recursion vs Loop

| Recursion | Loop |
|-----------|------|
| Method calls itself | Repeats using loops |
| Needs a base case | Needs a loop condition |
| Uses more memory | Uses less memory |
| Easier for recursive problems | Better for simple repetition |

---