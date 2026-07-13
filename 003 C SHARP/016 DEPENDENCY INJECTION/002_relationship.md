
# RELATIONSHIPS IN OOP

- A relationship defines how different classes/objects are connected and interact with each other.


**Types of Relationships :**
- IS-A Relationship (Inheritance)

- HAS-A Relationship (Composition / Aggregation)

# HAS-A Relationship (Composition / Aggregation)

**Meaning:**
- One class contains another class

**Example :**
```cs
class Engine
{
    public void Start()
    {
        Console.WriteLine("Engine started");
    }
}
class Car
{
    private Engine engine = new Engine(); // HAS-A
    public void StartCar()
    {
        engine.Start();
    }
}
```
- Car has an Engine

**Features :**
* Uses object inside class
* Promotes code reuse
* More flexible than inheritance


Real-life examples:
* Car has an Engine
* Student has a Book
* House has a Room


**Types of HAS-A Relationship**

- Composition (Strong relationship)
- Aggregation (Weak relationship)


### Composition (Strong relationship)
- Object cannot exist independently
- Tightly Coupled

```cs
using System;

class Engine
{
    public Engine()
    {
        Console.WriteLine("Engine Created");
    }
}

class Car
{
    private Engine engine;

    public Car()
    {
        engine = new Engine(); // created inside → strong relation
        Console.WriteLine("Car Created");
    }
}

class Program
{
    static void Main()
    {
        Car c = new Car();
    }
}
```



### Aggregation (Weak relationship)

- Object can exist independently
- Loosely Coupled

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
    private Engine engine;

    public Car(Engine eng) // passed from outside
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
        Engine e = new Engine(); // independent object
        Car c = new Car(e);      // injected

        c.StartCar();
    }
}
```

# IS-A Relationship (Inheritance)

**Meaning :**
- One class is a type of another class

Used for:
* Inheritance
* Code reuse

**Example:**
```cs
class Animal
{
    public void Eat()
    {
        Console.WriteLine("Eating...");
    }
}
class Dog : Animal  // IS-A
{
    public void Bark()
    {
        Console.WriteLine("Barking...");
    }
}
```
- Dog is an Animal

**Features :**
* Uses : (inheritance)
* Supports polymorphism
* Reuse parent class code


Real-life examples:
* Car is a Vehicle
* Dog is an Animal
* Student is a Person

###### Difference: IS-A vs HAS-A

Feature	IS-A	HAS-A
Type	Inheritance	Composition/Aggregation
Meaning	“is a”	“has a”
Reuse	Through parent class	Through object
Coupling	Tight	Loose
Example	Dog is Animal	Car has Engine


##### When to Use :
**Use IS-A when :**
* There is hierarchy
* You need inheritance
* Relationship is permanent

**Use HAS-A when :**
* One class uses another
* Need flexibility
* Want loose coupling


**Advantages :**
- Code reuse
- Better design
- Easy maintenance
- Real-world modeling

**Simple Understanding :**
- IS-A → Inheritance (type relationship)
- HAS-A → Containment (part relationship)
