# Coupling in OOP :

**Coupling means :**
- How strongly two classes depend on each other


### Tightly Coupled

**eaning :* ***
- One class is strongly dependent on another class
- If one changes → other also breaks


**Example :** Tightly Coupled
```cs
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
```
**Why tightly coupled?**
* Car creates Engine itself
* Cannot replace Engine easily
* Hard to test and modify


### Loosely Coupled

**Meaning :**
- Classes are independent
- One class depends on abstraction (interface), not concrete class

**Example :** Loosely Coupled
```cs
using System;

class PetrolEngine
{
    public void Start()
    {
        Console.WriteLine("Petrol Engine Started");
    }
}

class DieselEngine
{
    public void Start()
    {
        Console.WriteLine("Diesel Engine Started");
    }
}

class Car
{
    private PetrolEngine engine;

    public Car(PetrolEngine eng) // directly depends on PetrolEngine
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
        PetrolEngine engine = new PetrolEngine();
        Car car = new Car(engine);

        car.StartCar();
    }
}
```
**Better Version with Interface :**

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

class DiselEngine : IEngine
{
    public void Start()
    {
        Console.WriteLine("Disel Engine Started");
    }
}

class Car
{
    private IEngine engine;

    public Car(IEngine eng) // dependency injection
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
        IEngine engine = new PetrolEngine();
        Car car = new Car(engine);

        car.StartCar();
    }
}
```

**Why loosely coupled?**
* Car does NOT depend on PetrolEngine directly
* Can replace with DieselEngine, ElectricEngine easily
* Flexible and maintainable


------------------------------------------------

**Key Difference :**

Feature	Tightly Coupled	Loosely Coupled
Dependency	High	Low
Flexibility	Low	High
Change impact	High	Low
Testing	Difficult	Easy
Reuse	Limited	Better

**Relation topic :**

- Composition (strong relation) → often tightly coupled
- Aggregation (weak relation) → often loosely coupled

**Simple Understanding :**
- Tightly coupled = hard connection
- Loosely coupled = flexible connection

