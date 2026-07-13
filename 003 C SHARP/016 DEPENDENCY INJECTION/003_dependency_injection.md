
# DEPENDENCY INJECTION (DI) – FULL NOTE


**What is Dependency Injection?**

- Dependency Injection (DI) is a design pattern where a class does not create its dependencies itself.
- Instead, dependencies are provided (injected) from outside.
- “Don’t create objects, receive them.”


**Why DI is needed?**

- Problem without DI (Tight Coupling)
```cs
using System;
class Engine
{
    public void Start()
    {
        Console.WriteLine("Engine Started");
    }
}
class Car
{
    private Engine engine = new Engine(); // tightly coupled
    public void StartCar()
    {
        engine.Start();
    }
}
class Program
{
    static void Main()
    {
        Car car = new Car();
        car.StartCar();
    }
}
```
**Problems:**
* Cannot change Engine easily
* Hard to test
* Not flexible


With DI (Loose Coupling)
```cs
using System;
interface IEngine
{
    void Start();
}
class PetrolEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Petrol Engine Started");
    }
}
class DieselEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Diesel Engine Started");
    }
}
class Car
{
    private IEngine engine;
    public Car(IEngine eng) // dependency injected
    {
        engine = eng;
    }
    public void StartCar()
    {
        engine.Start();
    }
}
class Program
{
    static void Main()
    {
        IEngine engine = new PetrolEngine(); // choose engine
        Car car = new Car(engine);
        car.StartCar();
    }
}
```

## Types of Dependency Injection

### Constructor Injection

- Dependency is passed via constructor

```cs
using System;

// Step 1: Interface (abstraction)
interface IEngine
{
    void Start();
}

// Step 2: Implementations
class PetrolEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Petrol Engine Started");
    }
}

class DieselEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Diesel Engine Started");
    }
}

// Step 3: Class using dependency
class Car
{
    private IEngine engine;

    // Constructor Injection
    public Car(IEngine eng)
    {
        engine = eng;
    }

    public void StartCar()
    {
        engine.Start();
    }
}

// Step 4: Main Program
class Program
{
    static void Main()
    {
        // Choose dependency
        IEngine engine = new PetrolEngine();
        // IEngine engine = new DieselEngine(); // just change this line

        // Inject dependency
        Car car = new Car(engine);

        car.StartCar();
    }
}
```
- Required dependency
- Safe and recommended

### Property Injection
```cs
using System;

// 1. Interface (abstraction)
interface IEngine
{
    void Start();
}

// 2. Implementations
class PetrolEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Petrol Engine Started");
    }
}

class DieselEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Diesel Engine Started");
    }
}

// 3. Class using Property Injection
class Car
{
    // Dependency is set via property
    public IEngine Engine { get; set; }

    public void StartCar()
    {
        // safety check (important in property injection)
        if (Engine == null)
        {
            Console.WriteLine("Engine is not set!");
            return;
        }

        Engine.Start();
    }
}

// 4. Main Program
class Program
{
    static void Main()
    {
        Car car = new Car();

        // Inject dependency via property
        car.Engine = new PetrolEngine();
        // car.Engine = new DieselEngine(); // try switching

        car.StartCar();
    }
}
```
- Risk: Engine may be null


### Method Injection
```cs
using System;

interface IEngine
{
    void Start();
}

class PetrolEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Petrol Engine Started");
    }
}

class Car
{
    // Method Injection
    public void StartCar(IEngine engine)
    {
        engine.Start();
    }
}

class Program
{
    static void Main()
    {
        Car car = new Car();

        // Inject dependency at method call
        car.StartCar(new PetrolEngine());
    }
}
```

- .NET automatically injects dependency

-------------------------------------------------

## Service Lifetimes

##### Transient
```cs
services.AddTransient<IEngine, PetrolEngine>();
```
- New object every time

##### Scoped
```cs
services.AddScoped<IEngine, PetrolEngine>();
```
- One object per request

##### Singleton
```cs
services.AddSingleton<IEngine, PetrolEngine>();
```
- Single instance for entire app


**Advantages of DI:**

- Loose coupling
- Easy testing (mocking)
- Reusable code
- Easy maintenance
- Flexible design


**DI vs Without DI:** 

| Feature     | Without DI | With DI |
|------------|------------|---------|
| Coupling   | Tight      | Loose   |
| Flexibility| Low        | High    |
| Testing    | Hard       | Easy    |
| Maintenance| Difficult  | Easy    |

-------------------------------------

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