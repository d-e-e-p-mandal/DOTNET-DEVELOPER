
# What is virtual keyword?

- In C#, virtual means: “This method can be overridden in a derived (child) class.”
```cs
public virtual void FunctionName()
```
* Defined in parent class
* Gives permission to child class to change its behavior


# What is override keyword?

- Used in child class to modify (override) the parent class method
```cs
public override void FunctionName()
```
* Must match method signature
* Provides new implementation

- Method is overridden at runtime (runtime polymorphism)

-----------------------

### Is virtual and override keyword compulsory? 
- Yes, for overriding

- If you remove virtual but use Override : Generate Error
- If do not use virtual and override both : Method Hiding
```cs
class A
{
    public void Show()   // no virtual
    {
        Console.WriteLine("Parent");
    }
}
```
- Then this will cause error:
```cs
class B : A
{
    public override void Show() // ERROR
}
```
- Error: no suitable method found to override

```cs
class B : A
{
    public void Show()   // no override
}
```
- This is not overriding, it’s method hiding
