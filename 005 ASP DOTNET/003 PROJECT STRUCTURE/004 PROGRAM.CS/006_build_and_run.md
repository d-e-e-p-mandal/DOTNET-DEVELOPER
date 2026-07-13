
## builder.Build() :
Great 👍 now let’s clearly understand app.Build() (i.e., builder.Build()).


📘 **What is builder.Build()? :**

var app = builder.Build();

**It means :**

Convert configuration into a runnable application (WebApplication)

**Simple Meaning :**

Register → Configure → Build → Run

**Build() = prepare everything before starting serve r**

**Before Build() :**

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddScoped<IEmployeeService, EmployeeService>();

**At this stage :**

Services are only REGISTERED ❗
App is NOT running yet

## What Build() does internally

#### 1️⃣ Create ServiceProvider (DI Container)

**Converts :**

IServiceCollection → IServiceProvider

**Now DI can :**

Create objects (resolve dependencies)


#### 2️⃣ Finalize Configuration

**Reads :**
	•	appsettings.json
	•	Environment variables
	•	Command-line args


#### 3️⃣ Create Middleware Pipeline

**All middleware gets prepared :**
```cs
app.UseHttpsRedirection();
app.UseAuthorization();
```
Pipeline is built internally


#### 4️⃣ Create WebApplication Object
```cs
var app = builder.Build();
```
>> Now you get: Fully configured app object


**Internal Code (Simplified) :**

Conceptually:
```cs
public WebApplication Build()
{
    var serviceProvider = services.BuildServiceProvider();

    var app = new WebApplication(serviceProvider);

    return app;
}
```

**Flow :**
```
builder (configuration stage)
      ↓
Build()
      ↓
Create DI container
      ↓
Prepare middleware
      ↓
Return app
```

**After Build() :**
```cs
app.UseHttpsRedirection();
app.UseAuthorization();
app.MapControllers();
```

**Now you are :** Configuring request pipeline


**Important Rule :** Build() must be called BEFORE Run()

```cs
var app = builder.Build();
app.Run();
```

⸻
**Real-Life Analogy :**

Think:
	•	builder = ingredients 🍳  
	•	Build() = cooking 🍲  
	•	app = ready dish 🍽️  

Key Points :

✅ Build creates DI container
✅ Build prepares middleware
✅ Build returns app object
❌ Does NOT start server

**Final Understanding :**

Build = prepare application
Run   = start application



- builder.Build() creates the application by finalizing services, configuration, and middleware pipeline.

>Super Simple  
Build → ready app  
Run   → start app  



----



# What is app.Run()?

`app.Run();`

It means : Start the web server and begin listening for HTTP requests

⸻

**High-Level Flow :**

app.Run()
   ↓
Start Kestrel server
   ↓
Wait for HTTP requests
   ↓
Process requests using middleware pipeline


⸻

**Internal Code (Simplified) :**

Actual .NET code is complex, but conceptually it works like this:
```cs
public void Run()
{
    StartServer(); // start Kestrel

    while (true)
    {
        var request = WaitForRequest();

        ProcessRequest(request);
    }
}
```


**Real ASP.NET Core Internal Flow :**
```
app.Run()
   ↓
IHost.Run()
   ↓
StartAsync()
   ↓
Kestrel Server starts
   ↓
Listen on port (5000 / 5001)
```

**Internally calls (real structure) :**
```cs
public void Run()
{
    try
    {
        StartAsync().Wait(); // start server
        WaitForShutdown();   // keep app running
    }
    finally
    {
        StopAsync().Wait(); // cleanup
    }
}
```

### What happens step-by-step

1️⃣ Build completed

var app = builder.Build();

2️⃣ Run called

app.Run();

3️⃣ Server starts

Kestrel server starts listening

4️⃣ Request comes

GET /api/employee

5️⃣ Pipeline executes

Middleware → Routing → Controller

6️⃣ Response sent

JSON response returned


7️⃣ Loop continues

Server keeps running (infinite loop)


**Middleware Pipeline Execution :**
```
Request
   ↓
UseHttpsRedirection
   ↓
UseAuthorization
   ↓
MapControllers
   ↓
Controller Action
   ↓
Response
```

##### Important Point

`app.Run() `blocks the thread

**Means :** Code after app.Run() will NOT execute

**Example :**
```cs
app.Run();

Console.WriteLine("Hello"); // ❌ never runs
```

**Real Analogy :**

Think:
	•	app.Run() = turning ON server machine

Turn on → wait for requests → process → repeat


**Kestrel Server Role :**

`Kestrel is the default web server`

Handles HTTP requests
Manages connections


Final Understanding
```cs
app.Run() = start server + handle requests continuously
```

- `app.Run() `starts the web server and begins processing incoming HTTP requests through the middleware pipeline.

**Simple :**

Run → Start server → Listen → Process → Repeat
