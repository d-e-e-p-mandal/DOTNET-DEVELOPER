
## What is Lifetime?

Lifetime = How long an object lives (exists) in application

In ASP.NET Core there are 3 Lifetimes
1. Transient
```cs
builder.Services.AddTransient<MyService>();
```

2. Scoped
```cs
builder.Services.AddScoped<MyDbContext>();
```

3. Singleton

```cs
builder.Services.AddSingleton<CacheService>();
```

### Transient Lifetime

builder.Services.AddTransient<IService, Service>();

**Meaning :** New object created every time it is requested

Controller → Service → NEW instance
Another class → Service → NEW instance

👉 Even in same request:

Multiple calls → Multiple objects ❗

>Use when:  
	•	Lightweight service  
	•	No shared state  


### Scoped Lifetime

builder.Services.AddScoped<IService, Service>();

**Meaning :** One object per HTTP request

**Example :**  
Request 1 → 1 object
Request 2 → new object

**Inside same request :**  

Controller + Service → SAME instance

>Use when:  
	•	Database (DbContext)  
	•	Request-based operations  

⸻

### Singleton Lifetime

builder.Services.AddSingleton<IService, Service>();

**Meaning :** One object for entire application lifetime

**Example :**  
App start → object created
All requests → SAME object reused

>⚠️ Use when:  
	•	Shared data  
	•	Caching  

----

Comparison Table

Lifetime -> Instance Creation -> Scope  
Transient -> Every time	-> Short  
Scoped -> Per request -> Medium  
Singleton -> Once -> Whole app  

**Visual Flow :**

Request 1:
Transient → A, B, C (many)
Scoped    → X (one)
Singleton → S (same)

Request 2:
Transient → D, E, F (new)
Scoped    → Y (new)
Singleton → S (same)


**Important Notes :**

- ❗ Never inject Scoped into Singleton
- ❗ Singleton must be thread-safe
- ❗ Scoped is best for DB


**Final Understanding :**  
- Transient = always new	   
- Scoped    = per request	  
- Singleton = one for app	   


- Service lifetime defines how long a service instance lives in the application: transient (new each time), scoped (per request), and singleton (one per application).


**Simple :**
- Transient → many
- Scoped → one per request
- Singleton → one forever



**Custom Code Of All (For Undersstanding) :**
```cs
using System;

class Engine
{
    public Guid Id = Guid.NewGuid(); // unique ID
}

class Container
{
    private static Engine singletonInstance; // for Singleton
    private Engine scopedInstance;           // for Scoped

    // Transient → new every time
    public Engine GetTransient()
    {
        return new Engine();
    }

    // Singleton → same for whole app
    public Engine GetSingleton()
    {
        if (singletonInstance == null)
            singletonInstance = new Engine();

        return singletonInstance;
    }

    // Scoped → same within one scope
    public Engine GetScoped()
    {
        if (scopedInstance == null)
            scopedInstance = new Engine();

        return scopedInstance;
    }

    // Reset scope
    public void NewScope()
    {
        scopedInstance = null;
    }
}

class Program
{
    static void Main()
    {
        Container c = new Container();

        // TRANSIENT
        Console.WriteLine( TRANSIENT");
        var t1 = c.GetTransient();
        var t2 = c.GetTransient();
        Console.WriteLine($"t1: {t1.Id}");
        Console.WriteLine($"t2: {t2.Id}");

        // SINGLETON
        Console.WriteLine("\n🔷 SINGLETON");
        var s1 = c.GetSingleton();
        var s2 = c.GetSingleton();
        Console.WriteLine($"s1: {s1.Id}");
        Console.WriteLine($"s2: {s2.Id}");

        // SCOPED (Same Scope)
        Console.WriteLine("\n🔷 SCOPED (Same Scope)");
        var sc1 = c.GetScoped();
        var sc2 = c.GetScoped();
        Console.WriteLine($"sc1: {sc1.Id}");
        Console.WriteLine($"sc2: {sc2.Id}");

        // SCOPED (New Scope)
        Console.WriteLine("\n🔷 SCOPED (New Scope)");
        c.NewScope();
        var sc3 = c.GetScoped();
        Console.WriteLine($"sc3: {sc3.Id}");
    }
}
```