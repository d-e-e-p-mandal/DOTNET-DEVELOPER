# Delegates in C#

---

# What is a Delegate?

A **Delegate** is a type that holds a reference to a method.

It allows a method to be passed as a parameter and called indirectly.

A delegate can point to one or more methods having the **same return type and parameter list**.

---

# Why Use Delegates?

Delegates are used to:

- Call methods indirectly.
- Pass methods as arguments.
- Implement callbacks.
- Support events and event handling.

---

# Delegate Declaration

### Syntax

```csharp
delegate returnType DelegateName(parameters);
```

### Example

```csharp
delegate void Message();
```

---

# Delegate Basics

First, declare a delegate.

Then create a delegate object and assign a method to it.

Finally, invoke the delegate.

### Example

```csharp
using System;

delegate void Message();

class Program
{
    static void Hello()
    {
        Console.WriteLine("Hello C#");
    }

    static void Main()
    {
        Message msg = Hello;

        msg();
    }
}
```

**Output**

```text
Hello C#
```

---

# Single Cast Delegate

A **Single Cast Delegate** points to only **one method**.

### Example

```csharp
using System;

delegate void Print();

class Program
{
    static void Display()
    {
        Console.WriteLine("Single Cast Delegate");
    }

    static void Main()
    {
        Print p = Display;

        p();
    }
}
```

**Output**

```text
Single Cast Delegate
```

---

# Multicast Delegate

A **Multicast Delegate** points to **multiple methods**.

Use the `+` or `+=` operator to add methods.

Use the `-=` operator to remove methods.

### Example

```csharp
using System;

delegate void Print();

class Program
{
    static void Hello()
    {
        Console.WriteLine("Hello");
    }

    static void Welcome()
    {
        Console.WriteLine("Welcome");
    }

    static void Main()
    {
        Print p = Hello;

        p += Welcome;

        p();
    }
}
```

**Output**

```text
Hello
Welcome
```

---

# Removing a Method

```csharp
Print p = Hello;

p += Welcome;

p -= Hello;

p();
```

**Output**

```text
Welcome
```

---

# Anonymous Methods

An **Anonymous Method** is a method without a name.

It is created using the `delegate` keyword.

### Example

```csharp
using System;

delegate void Message();

class Program
{
    static void Main()
    {
        Message msg = delegate ()
        {
            Console.WriteLine("Anonymous Method");
        };

        msg();
    }
}
```

**Output**

```text
Anonymous Method
```

---

# Advantages of Delegates

- Reusable code
- Flexible method calling
- Supports callbacks
- Used in event handling
- Supports multicast functionality

---

# Difference Between Single Cast and Multicast Delegate

| Single Cast Delegate | Multicast Delegate |
|----------------------|--------------------|
| Refers to one method | Refers to multiple methods |
| Calls one method | Calls all assigned methods |
| Simple to use | Used for events and callbacks |

---
