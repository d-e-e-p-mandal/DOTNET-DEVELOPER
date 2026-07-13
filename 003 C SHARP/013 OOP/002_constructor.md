## Constructor :
- It's a special method present under a class.
- It is responsible for initializing the variables of that class.
- The name of the Constructor method is exactly the same name of the class in which it was present.
- It is non-value returning method
- **Each and every class requires this constructor** if we want to create the instance of that class. If not defined explicitly and with the help of that implicit constructor instance of class can be created.

**Note :** 
- Defining : Implicit or Explicit
- Calling : Explicit
- If we do not define constructor then complier define implicit(default) constructor.

#### Implicitly Constructor :
- Implicityly defined constructors are **parameter-less** and these constructors are also known as default constructors.

```cs
using System;

public class A
{
    public int x = 10; // no constructor written
}

public class Program
{
    public static void Main()
    {
        A obj = new A(); // implicit constructor called
        Console.WriteLine(obj.x);
    }
}
```


#### Explicitly Defined Constructor :
- Implicitly defined constructor are public.
- We can also define a constructor under the class and if we define it we can call it as explicit constructor and explicit constructor can be parameter less or parameterized also.



Structure :
```cs
[<modifiers(public)>]<ClassName>([<parameter list>]) {
    //statements
}
```
## Type of Constructor :
1. Default Constructor
2. Parameterized Constructor.
3. Copy Constructor
4. Static Constructor

#### Default Constructor :
- Can be defined by excplicitly or else will be default implicitly provided there is no explicit constructor under the class.
- If a constructor method doesn't take any parameters then we call that as default or parameter less.

Example : Implicit
```cs
using System;

public class A
{
    public int x = 10; // no constructor written
}

public class Program
{
    public static void Main()
    {
        A obj = new A(); // implicit constructor

        Console.WriteLine(obj.x);
    }
}
```

Example : Explicit
```cs
using System;

public class A
{
    public int x;

    // explicit default constructor
    public A()
    {
        x = 20;
    }
}

public class Program
{
    public static void Main()
    {
        A obj = new A();

        Console.WriteLine(obj.x);
    }
}
```

#### Parameterized Constructor :
- If a constructor method is defined with out any parameters we call that as parameterized constructor and these constructors can be defined by the programmers only but never can be defined implicitly.

```cs
using System;

public class Sum
{
    // constructor for 2 values
    public Sum(int a, int b)
    {
        Console.WriteLine("Sum (a+b) = " + (a + b));
    }

    // constructor for 3 values
    public Sum(int a, int b, int c)
    {
        Console.WriteLine("Sum (a+b+c) = " + (a + b + c));
    }
}

public class Program
{
    public static void Main()
    {
        new Sum(10, 20);      
        new Sum(10, 20, 30);  
    }
}
```

#### Copy Constructor :

- If we want to create multiple instances with the same values then we use these copy constructors, in a copy constructor the constructor take the same class as a paramter to it.

```cs
using System;

public class A
{
    int x;

    // parameterized constructor
    public A(int value)
    {
        x = value;
    }

    // copy constructor
    public A(A obj)
    {
        x = obj.x; // copy value
    }

    public void Show()
    {
        Console.WriteLine("Value = " + x);
    }
}

public class Program
{
    public static void Main()
    {
        A obj1 = new A(50);   // original object
        A obj2 = new A(obj1); // copy object

        obj1.Show();
        obj2.Show();
    }
}
```

#### Static Constructor

- If a constructor is explicitly declared by using static we call that as static constructor.
- Static constructors are responsible for initializing static variables. They are never called explicitly. They are called implicitly by the runtime and are executed first when the class is accessed.
- Static constructor runs first 
- No over loading (No parameters)

Static constructor rules:
- Must be static
- Must NOT have public/private/protected ❗
- No parameters 
- Only one allowed


```cs
using System;

public class A
{
    static int x;

    static A()
    {
        x = 100;
        Console.WriteLine("Static constructor called");
    }

    public void Show()
    {
        Console.WriteLine(x);
    }
}

class Program
{
    static void Main()
    {
        A obj = new A(); // triggers static constructor
        obj.Show();
    }
}
```