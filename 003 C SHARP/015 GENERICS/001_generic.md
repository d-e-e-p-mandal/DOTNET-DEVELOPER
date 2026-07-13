
# Generics in C# 

**What are Generics?**

- Use <T> as placeholder
- Generics allow you to write **type-safe and reusable code** by using a placeholder for data type.

- Instead of using fixed types like `int`, `string`, we use a **type parameter (T)**. *T is identifier (we can declare any word but T is recomended. T stand here for type)*

**Why Generics?**
- Code reusability  
- Type safety  
- Better performance (no boxing/unboxing)  
- Compile-time error checking  

**Use Case :**
- Used in collections and methods
- Avoids runtime errors
- Improves performance
- Supports multiple type parameters


**Basic Syntax :**

**Generic in Function :**
```cs
using System;
class Helper
{
    public T Show<T>(T data)
    {
        return data;
    }
}

class Program
{
    static void Main()
    {
        Helper h = new Helper();   // create object

        Console.WriteLine(h.Show<int>(10));
        Console.WriteLine(h.Show<string>("Hello"));
    }
}
```

Output : 
```
10
Hello
```

**Generic Type in CLass :**
Example 1 :

```csharp
class ClassName<T>
{
    public T data;
}
```
Usage:
```cs
Test<int> obj1 = new Test<int>();
obj1.value = 10;

Test<string> obj2 = new Test<string>();
obj2.value = "Hello";
```

**Without Generics : Problem**
```cs
class Test
{
    public object data;
}
```
Issues:
- No type safety
- Requires casting
- Runtime errors possible


Example 2 :
```cs
using System;
// Generic Class
class Test<T>
{
    public T value;
}
// Main Class
class Program
{
    // Generic Function using Generic Class
    public static void ShowData<T>(T input)
    {
        Test<T> obj = new Test<T>();  // create generic class object
        obj.value = input;

        Console.WriteLine(obj.value);
    }

    static void Main()
    {
        ShowData<int>(10);
        ShowData<string>("Hello");
    }
}
```

**Benefits:**
- Type-safe
- No casting
- Compile-time checking


### Multiple Input Generic Class

**Example :**
```cs
class MyKeyValuePair<T, U>
{
    public T Key;
    public U Value;
}
```

### Example with Constraint
```cs
class Test<T> where T : new()
{
    public T Create()
    {
        return new T();
    }
}
```

### Generic Interface
```cs
interface ITest<T>
{
    void Show(T value);
}
```

### Generic Delegate
```cs
delegate T MyDelegate<T>(T value);
```



**Advantages of Generics :**
	•	Type safety
	•	Reusable code
	•	Better performance
	•	No casting required
	•	Compile-time checking

⸻
**Disadvantages :**
	•	Slightly complex syntax
	•	Hard for beginners

⸻
**Generics vs Non-Generics :**

Feature	Generic	Non-Generic
Type safety	Yes	No
Casting	Not required	Required
Performance	Fast	Slower
Errors	Compile-time	Runtime


