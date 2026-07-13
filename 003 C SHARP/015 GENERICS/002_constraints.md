# Constraints in Generics
- Used to restrict type of T

### Allowed Constraints
1. Reference type
```cs
where T : class
```

2. Value type
```cs
where T : struct
```

3. Specific base class : Any class(ClassName) and it's all child class
```cs
where T : Product // className
```

4. Interface
```cs
where T : interface
```

5. Specific Interface :
```cs
where T : IDisposable
```

6. Default constructor
```cs
where T : new()
```

7. Multiple constraints
```cs
where T : Product, IDisposable, new()
```



**Example :** Custom Type Allow : Specific class (Base Class)
- If a specific class allow then it's all child or derived class allowed.

```cs
using System;
using System.Collections.Generic;

class Product
{
    public int ProductId { get; set; }
    public string Name { get; set; }
}

// T must be Product or derived from Product
class ProductStore<T> where T : Product
{
    private Dictionary<int, T> products = new Dictionary<int, T>();

    public void Add(T item)
    {
        products[item.ProductId] = item;
    }

    public T Get(int id)
    {
        return products.ContainsKey(id) ? products[id] : null;
    }

    public void ShowAll()
    {
        foreach (var p in products)
        {
            Console.WriteLine(p.Key + " - " + p.Value.Name);
        }
    }
}

class Program
{
    static void Main()
    {
        ProductStore<Product> store = new ProductStore<Product>();

        store.Add(new Product { ProductId = 1, Name = "Laptop" });
        store.Add(new Product { ProductId = 2, Name = "Mobile" });

        Console.WriteLine(store.Get(1).Name);

        store.ShowAll();
    }
}
```

**Output :**
```
Laptop
1 - Laptop
2 - Mobile
```

Example :Child Class : Only Product or its child classes allowed

```cs
class ElectronicProduct : Product
{
    public string Brand { get; set; }
}
```
```cs
ProductStore<ElectronicProduct> store = new ProductStore<ElectronicProduct>();
```


### Not Allowed Constraints

1. Specific primitive types
```cs
where T : int      
where T : string   
where T : double   
```

2. Specific object instances
```cs
where T : obj    
```

3. Mixed invalid combinations
```cs
where T : struct, class   
```

4. Constructor with parameters
```cs
where T : new(int)   //not allowed
```

-----------------------


### Extended new() In Generic of C# :

- where T : new() means:
- T must have a Default constructor - explicit or implicit
- Order matters → new() must be last`

**Valid List :**

1. With class (reference type)
```cs
where T : class, new()
```
- T must be a reference type and have default constructor


2. With base class
```cs
where T : Product, new()
```
- T must inherit Product and have default constructor

3. With interface
```cs
where T : IDisposable, new()
```

**Example :**
```cs
using System;

// Product class (has default constructor ✔)
class Product
{
    public string Name = "Hi";
    // implicit
    public Product()
    {
        Name = "Default Product";
    }
}

// Generic class with constraint
class Factory<T> where T : new()
{
    public T Create()
    {
        return new T();   // must be possible
    }
}

class Program
{
    static void Main()
    {
        Factory<Product> f = new Factory<Product>();

        Product p = f.Create();

        Console.WriteLine(p.Name);
    }
}
```


**Invalid List :**

🔥 Important Rules

1. new() must be last
```cs
where T : new(), class   // x
```
2. Cannot combine with struct
```cs
where T : struct, new()   // x
```

- All structs already have a default constructor
- compiler error


