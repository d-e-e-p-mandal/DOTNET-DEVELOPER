# OOP :
-----------------------------------------------

## Class :
- It is a user defined type.
- class is a blueprint of Object.

**Variable of a Class :** A copy of the class that is not initialized.
```cs
class A {
    int x;
}
class Program
{
    static void Main()
    {
        A a;
    }
}
```

**Instance of a class :** 
- A copy of the class that is initialized by using the new keyword.
- Every Instance have seperate memory allocation.
```cs
class A {
    int x;
}
class Program
{
    static void Main()
    {
        A a = new A();
    }
}
```

**Reference of a Class :**  
- Aa copy of the class that is initialized by using an existing instance and references of class will not have any memory allocation they will be sharing the same memory of the instance that assigned for initializing the variable.
- Reference of a clas can be called as a pointer to the instance and every modification we perform on the members using instance reflects when we acess those members through refference and vice-versa

```cs
class A {
    int x;
}
class Program
{
    static void Main()
    {
        A a = new A();
        A b;
        b = a;   // 
    }
}
```
**Object :**
- It is a instance of class


```cs
using System;

class Student
{
    public string name;
}

class Program
{
    static void Main()
    {
        Student s1 = new Student();  // object created
        s1.name = "Deep";

        Console.WriteLine(s1.name);
    }
}
```

## Types Of Classes In C#

### Simple Class

- Basic  class used to create objects

```cs
class A
{
    public void Show()
    {
        Console.WriteLine("Normal Class");
    }
}
```
**Usage :**
```cs
A obj = new A();
obj.Show();
```


### Static Class

- Canno t create object, only static members

```cs
static class A
{
    public static void Show()
    {
        Console.WriteLine("Static Class");
    }
}
```
**Usage :**
```cs
A.Show(); // no object
```

### Abstract Class

- Canno t create object, used for inheritance
- atleast one abstruct function.

```cs
abstract class A
{
    public abstract void Show();
}

class B : A
{
    public override void Show()
    {
        Console.WriteLine("Abstract Class");
    }
}
```
**Usage :**
```cs
A obj = new B();
obj.Show();
```

### Sealed Class

- Cannot be inherited

```cs
sealed class A
{
    public void Show()
    {
        Console.WriteLine("Sealed Class");
    }
}
```
- Inheritance Not allowed :
```cs
class B : A {} // ERROR
```


### Partial Class

- Class  split into multiple files

```cs
partial class A
{
    public void Show1()
    {
        Console.WriteLine("Part 1");
    }
}

partial class A
{
    public void Show2()
    {
        Console.WriteLine("Part 2");
    }
}
```
**Usage :**
```cs
A obj = new A();
obj.Show1();
obj.Show2();
```


### 6️⃣ Nested Class

- Class inside another class

```cs
class Outer
{
    public class Inner
    {
        public void Show()
        {
            Console.WriteLine("Nested Class");
        }
    }
}
```
Usage:
```cs
Outer.Inner obj = new Outer.Inner();
obj.Show();
```



**Summary :**

- Normal → create object
- Static → no object
- Abstract → for inheritance
- Sealed → no inheritance
- Partial → split class
- Nested → class inside class

