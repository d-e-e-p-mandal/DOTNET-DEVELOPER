# Async Programming in .NET (C#)

Asynchronous programming allows your program to:
* Start a task
* Continue doing other work
* Come back when the task is finished
- Main goal: non-blocking execution

**Why use Async?**
* Improves performance
* Keeps UI responsive (no freezing)
* Efficient for I/O operations (API, DB, file)

### Core Keywords :

##### async :

- Marks a method as asynchronous
```cs
public async Task MyMethod()
{
}
```

##### await
- Waits for task without blocking thread
```cs
await Task.Delay(1000);
```

##### Task
- Represents an asynchronous operation
```cs
public async Task DoWork()
```

**Example :**
```cs
using System;
using System.Threading.Tasks;
class Program
{
    static async Task Main()
    {
        Console.WriteLine("Start");
        await Task.Delay(2000);
        Console.WriteLine("End");
    }
}
```

**How it works internally :**

`await:`
* Pauses method
* Frees thread
* Resumes later

**Thread vs Async :**

- Thread - Async
- Uses multiple threads	- Uses fewer threads
- Heavy - Lightweight
- Parallel - Concurrent


**When NOT to use Async :**
* Simple calculations
* CPU-bound work (use multithreading instead)


⚡ Final Summary

* async → marks method
* await → waits without blocking
* Task → async operation
* WhenAll → parallel execution

⸻

If you want next:

* 👉 async vs multithreading deep comparison
* 👉 real ASP.NET Core async API
* 👉 deadlock explanation (VERY IMPORTANT)

```cs
using System;
using System.Threading.Tasks;

class Car
{
    public async Task A()
    {
        Console.WriteLine("A started");
        await Task.Delay(3000);
        Console.WriteLine("A ended");
    }

    public async Task B()
    {
        Console.WriteLine("B started");
        await Task.Delay(3000);
        Console.WriteLine("B ended");
    }

    public async Task C()
    {
        Console.WriteLine("C started");
        await Task.Delay(3000);
        Console.WriteLine("C ended");
    }
}

class Program
{
    static async Task Main()
    {
        Car c = new Car();

        Console.WriteLine("Started");

        await Task.WhenAll(
            c.A(),
            c.B(),
            c.C()
        );

        Console.WriteLine("Ended");
    }
}
```

**Parallel Execution :**
```cs
await Task.WhenAll(
    Task1(),
    Task2(),
    Task3()
);
```
- Runs tasks concurrently