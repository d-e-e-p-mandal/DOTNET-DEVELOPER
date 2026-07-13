
# Variables in Class in C# (All Types)
- Instance Variable
- Static Variable
- const (Constant) 

#### Instance (Non-Static) Variable

- Each object has its own copy
- Runs every time a new object is created
- Instance variable can be initialized at declaration, inside constructor, or inside non-static method.
- Instance variable can be accessed using object name or from non-static methods.
```cs
class A
{
    public int x = 10; // instance variable
}
```

#### Static Variable

- It belongs to the class, not to objects.
- It is shared among all objects of the class.
- **Initilize :** Initialized at runtime when class is first used. Static variable can be initialized at declaration or inside static constructor.
- **Access :** It can be *accessed* using class name or from both static and non-static methods. 

```cs
using System;

class A
{
    public static int x = 10;

    // static method
    public static void ShowStatic()
    {
        Console.WriteLine(x); // ✔ allowed
    }

    // non-static method
    public void ShowInstance()
    {
        Console.WriteLine(x); // ✔ allowed
    }
}

class Program
{
    static void Main()
    {
        // direct access
        Console.WriteLine(A.x); // ✔ best way

        A.ShowStatic(); // ✔ static method

        A obj = new A();
        obj.ShowInstance(); // ✔ non-static method
    }
}
```

#### const (Constant)

- Fixed value (compile-time)
- ✔ Must assign at declaration
- ✔ Cannot change
- ✔ Always static internally
- Only ONE copy exists

```cs
class A
{
    public const int x = 10;
}
```

#### readonly (Instance)

- ✔ Value set at declaration or constructor
- ✔ Cannot change after initialization
- ✔ Runtime constant
- ✔ Can be instance or static
- Each object has separate copy
```cs
class A
{
    public readonly int x;

    public A(int value)
    {
        x = value; // allowed
    }
}
```

#### static readonly

- Value is assigned once at runtime and shared by all objects of the class.
- ✔ Belongs to class (static)
- ✔ Only ONE copy exists
- ✔ Value can be set only once
- Initilize At declaration or Inside static constructor 

```cs
class A
{
    public static readonly int x;

    static A()
    {
        x = 50;
    }
}
```

**Example (All Together) :**
```cs
using System;

class A
{
    public int a = 1;                  // instance
    public static int b = 2;           // static
    public const int c = 3;            // const
    public readonly int d;             // readonly
    public static readonly int e;      // static readonly

    // constructor
    public A()
    {
        d = 4;
    }

    // static constructor
    static A()
    {
        e = 5;
    }
}

class Program
{
    static void Main()
    {
        A obj1 = new A();
        A obj2 = new A();

        Console.WriteLine(obj1.a); // 1
        Console.WriteLine(A.b);    // 2
        Console.WriteLine(A.c);    // 3
        Console.WriteLine(obj1.d); // 4
        Console.WriteLine(A.e);    // 5
    }
}
```

### C# Variable Behavior Comparison

| Type | Static | Change | When Set |
| :--- | :---: | :---: | :--- |
| **Instance** | ❌ | ✔ | Runtime |
| **Static** | ✔ | ✔ | Runtime |
| **Const** | ✔ | ❌ | Compile-time |
| **Readonly** | ❌ | ❌ (after init) | Constructor |
| **Static Readonly** | ✔ | ❌ (after init) | Static constructor |



Important Points

✔ const is always static (no need to write static)
✔ readonly can be instance or static
✔ static readonly is shared + fixed after init
✔ instance variables are per object

