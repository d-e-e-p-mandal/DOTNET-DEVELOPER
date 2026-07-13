# Inheritance :

- It is mechanism of consuming the membembers of one class in another class by establishing parent/child relationship between the classes which provides re-usability.
- Parent class constructor must be accessible to the child class, otherwise inheritance will cause an error. 
- Parent class constructors execute first in hierarchical order during inheritance.
- `Child object takes memory of both parent and child.`

Terminalogy :
- Parent or Base or Super 
- Child or Derived
- Inheritance Relationship


**Purpose of Inheritance :**

- Code Reusability
- Reduce code duplication
- Improve maintainability
- Enable hierarchical classification


**Syntax :**
```cs
class Parent
{
}

class Child : Parent
{
}
```
**`:`→ inheritance symbol**

**Example :**
```cs
using System;

class A   // Parent
{
    public void Show()
    {
        Console.WriteLine("Parent Method");
    }
}

class B : A   // Child
{
    public void Display()
    {
        Console.WriteLine("Child Method");
    }
}

class Program
{
    static void Main()
    {
        B obj = new B();

        obj.Show();    // inherited
        obj.Display(); // own
    }
}
```

## Types of Inheritance :

**Single Inheritance :**  

`One parent → one child`
```cs
class A {}
class B : A {}
```

**Multilevel Inheritance :**  

`A → B → C`
```cs
class A {}
class B : A {}
class C : B {}
```

**Hierarchical Inheritance :**

One parent → multiple children
```cs
class A {}
class B : A {}
class C : A {}
```

**Multiple Inheritance : Not supported using classes in C#**

- Supported using interfaces

**Access Modifiers in Inheritance :**
```
Modifier	Accessible in Child
public	    - Yes
protected	- Yes
private	    - No
internal	- (same assembly)
```

**Example (Protected) :**
```cs
class A
{
    protected int x = 10;
}

class B : A
{
    public void Show()
    {
        Console.WriteLine(x);
    }
}
```

**Constructor in Inheritance :**
- Parent class constructors execute first in hierarchical order during inheritance.
- `Parent constructor runs first`.

```cs
class A
{
    public A()
    {
        Console.WriteLine("Parent");
    }
}

class B : A
{
    public B()
    {
        Console.WriteLine("Child");
    }
}
```

**base Keyword :**

- Used to access parent class
```cs
class A
{
    public void Show()
    {
        Console.WriteLine("Parent");
    }
}

class B : A
{
    public void Display()
    {
        base.Show();
    }
}
```

**Method Overriding :**

- Child modifies parent method
```cs
class A
{
    public virtual void Show()
    {
        Console.WriteLine("Parent");
    }
}

class B : A
{
    public override void Show()
    {
        Console.WriteLine("Child");
    }
}
```

**Advantages :**
- Code reuse
- Extensibility
- Easy maintenance
- Logical hierarchy


**Disadvantages :**
- Tight coupling
- Complex hierarchy
- Difficult debugging

**Real-Life Example :** Vehicle → Car → ElectricCar

**Important Rules :**

- Use ":" for inheritance
- Constructor of parent runs first
- Private members not inherited
- C# does not support multiple inheritance with classes
- Interfaces can achieve multiple inheritance


Final Understanding : Inheritance allows one class to reuse and extend functionality of another class






---------------------


### Reference of Class in Inheritance

Example:

```cs
using System;

class A
{
    public void Show()
    {
        Console.WriteLine("Parent");
    }
}

class B : A
{
    public void Display()
    {
        Console.WriteLine("Child");
    }
}

class Program
{
    static void Main()
    {
        A obj = new B();

        obj.Show();     // allowed
        // obj.Display(); // not allowed
    }
}
```

- Reference type (A) → decides what you can access ✔
- Object type (B) → decides what memory is created ✔

```cs
A obj = new B(); // reference of parent, object of child
```
```cs
B obj = new A(); // NOT allowed
```


**Why child method not accessible?**  
Reference = A  
So only A methods visible, child hidden


**2️⃣ Memory Concept**

When you write:
```cs
A obj = new B();
```
In Memory:

Heap: `[ A part ] + [ B part ]`  ✔ full object created

Stack: `obj → reference type A`


⸻

**Important Rule :**
- `Full object (parent + child) is created in memory`
- `But access depends on reference type`

**Does child object take parent memory?**

YES ✔

Child object = Parent part + Child part

**Visual :**
B object memory:
```
[ A (parent fields) ]
[ B (child fields) ]
```

----------------------------------------------------

# Parent class of all Class :

- Every class in C# has a default parent class called Object, and it can use its methods.
- All classes automatically inherit from `System.Object`
- No need to write explicitly

**Even if you don’t write :**
```cs
class A
{
}
```
**Internally it becomes :**
```cs
class A : Object
{
}
```

**What you get from Object?**

All classes can use methods like:
- ToString()
- Equals()
- GetHashCode()
- GetType()

📘 **Example**
```cs
using System;

class A
{
}

class Program
{
    static void Main()
    {
        A obj = new A();

        Console.WriteLine(obj.ToString()); // from Object
        Console.WriteLine(obj.GetType());  // from Object
    }
}
```
**Output :**
```
A
A
```

**Important Clarification**

- Every class has default parent (Object)
- But NOT all properties are inherited automatically
- Only accessible methods/members are usable


