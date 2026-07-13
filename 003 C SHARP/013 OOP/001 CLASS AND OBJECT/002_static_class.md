# Static Class in C# 

**A static class:**
* Cannot be instantiated (no new)
* Contains only static members
* Accessed using ClassName.Member


**Syntax Example :**
```cs
public static class Utility
{
    public static void ShowMessage()
    {
        Console.WriteLine("Hello from static class");
    }
}
```
Calling:
```cs
Utility.ShowMessage();
```

**Important Rule :**

##### All functions (methods) inside a static class MUST be static
This is allowed:
```cs
public static class Demo
{
    public static void Show()
    {
    }
}
```
This is NOT allowed:
```cs
public static class Demo
{
    public void Show() // ERROR
    {
    }
}
```

##### We can not create object

Not allowed:
```cs
Utility u = new Utility(); // ERROR
```

##### Constructor in static class

* Cannot have normal constructor
* Can have static constructor
```cs
public static class Demo
{
    static Demo()
    {
        Console.WriteLine("Static constructor called once");
    }
}
```

🔹 Full Example (Important)
```cs
using System;
public static class ApiResponseFactory
{
    public static string GetSuccessMessage()
    {
        return "Success";
    }
    public static string GetErrorMessage()
    {
        return "Error";
    }
}
class Program
{
    static void Main()
    {
        string msg1 = ApiResponseFactory.GetSuccessMessage();
        string msg2 = ApiResponseFactory.GetErrorMessage();
        Console.WriteLine(msg1);
        Console.WriteLine(msg2);
    }
}
```

##### Why use static class?
* You don’t need object
* You want shared/common logic
* Example:
    * Math functions
    * Helper methods
    * Factory methods


##### Example from .NET

**Example:** System.Math
```cs
int max = Math.Max(10, 20);
```
- Math is a static class
- No object created
- Direct call

