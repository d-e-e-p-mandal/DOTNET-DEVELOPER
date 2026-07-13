# Access Modifer/Specifiers :
- It is a special kind of modifers using which we can define the scope of a type and it's members.
- Define the scope (visibility) of a type and its members
- Who can access variables, methods, and classes

**Types of Access Modifer on Members:**  
- Public
- Private
- Internal
- Protected
- Protected Internal

**Type of Modifier on Class:**
Only two type class modifier exist in c#.
- Public
- Internal

```cs
public class A {}   // 1
internal class B{}   // 2
```
**Note :**  
- Default access modifier = Private (for class members)
- Default for class = Internal


#### Public Member Access Mododifier :
- Accessible from anywhere (any class, any project)
```cs
public class A
{
    public int x = 10;
}

class Program
{
    static void Main()
    {
        A obj = new A();
        Console.WriteLine(obj.x); // ✅ allowed
    }
}
```

### Private Member Access Mododifier :
- Accessible only within the same class
- Use seter and geter method.

Example : Method 1: Using Property (Recommended)
```cs
using System;

public class A
{
    private int x;

    public int X
    {
        get { return x; }
        set { x = value; }
    }
}

class Program
{
    static void Main()
    {
        A obj = new A();

        obj.X = 100; // setter
        Console.WriteLine(obj.X); // getter
    }
}
```

Example : Method 2 :
```cs
class A
{
    private int x = 10;
    // Getter
    public int GetX()
    {
        return x;
    }

    // Setter
    public void SetX(int value)
    {
        x = value;
    }

    public void Show()
    {
        Console.WriteLine(x); // ✅ allowed inside class
    }
}

class Program
{
    static void Main()
    {
        A obj = new A();
        obj.Show();
        // Console.WriteLine(obj.x); ❌ NOT allowed

        Console.WriteLine(obj.GetX()); // get value
        obj.SetX(50); // set values
        Console.WriteLine(obj.GetX()); // updated value

    }
}
```

### Protected Member Access Mododifier :
- Within class + derived (child) class

```cs
class A
{
    protected int x = 10;
}

class B : A
{
    public void Show()
    {
        Console.WriteLine(x); // ✅ allowed in child class
    }
}
```

### Internal Member Access Mododifier :
- Accessible within same project (assembly)
```cs
internal class A
{
    internal int x = 10;
}

class Program
{
    static void Main()
    {
        A obj = new A();
        Console.WriteLine(obj.x); // ✅ allowed (same project)
    }
}
```

### Protected Internal Member Access Mododifier :
- Same project OR derived class in another project
```cs
class A
{
    protected internal int x = 10;
}

class B : A
{
    public void Show()
    {
Console.WriteLine(x); // ✅ allowed (inheritance)
    }
}

class Program
{
    static void Main()
    {
        A obj = new A();
Console.WriteLine(obj.x); // allowed (same project)
    }
}
```

--- 

# Same Project :

📘 **What is Same Project? :**

- Same Project means All classes inside one application/project file (.csproj)

When you build project:
```
Project → becomes → Assembly (.exe / .dll)
```
So: Same Project = Same Assembly


**Simple Meaning :**

All files/classes inside one project = same project

**Example (Same Project) :**

// File1.cs
```cs
class A
{
    internal int x = 10;
}
```

// File2.cs
```cs
class B
{
    public void Show()
    {
        A obj = new A();
Console.WriteLine(obj.x); // allowed
    }
}
```

**Important Point :**

Same project does NOT depend on namespace ❗
It depends on assembly ✔

**Final Understanding :**

- Same project = same compiled output (assembly)
- Same project means classes belong to the same assembly (.exe/.dll)


#### How to use public members :
Imprort ProjectName :
```cs
using ProjectName; // import namespace
```


We have 2 projects :
- Project1 → contains class A
- Project2 → uses class A

**Step 1️⃣ Project1 Code :**
✔ Project Name (in Visual Studio)
✔ Default Namespace (auto created)
```cs
// Project1 (Class Library)

namespace Project1
{
    public class A
    {
        public int x = 10;

        public void Show()
        {
            Console.WriteLine("Hello from Project1");
        }
    }
}
```

**Step 2️⃣ Project2 Code :**

**Add reference of Project1 in Project 2**

// Project2
```cs
using System;
using Project1; // import namespace

class Program
{
    static void Main()
    {
        A obj = new A();

Console.WriteLine(obj.x); // allowed
obj.Show();               // allowed
    }
}
```

**Output :**
```
10
Hello from Project1
```




### C# Access Modifiers Visibility

| Modifier | Same Class | Same Project (Assembly) | Child Class (Derived) | Other Project |
| :--- | :---: | :---: | :---: | :---: |
| **Public** | ✅ | ✅ | ✅ | ✅ |
| **Private** | ✅ | ❌ | ❌ | ❌ |
| **Protected** | ✅ | ❌ | ✅ | ❌ |
| **Internal** | ✅ | ✅ | ❌ | ❌ |
| **Protected Internal** | ✅ | ✅ | ✅ | ❌ |

