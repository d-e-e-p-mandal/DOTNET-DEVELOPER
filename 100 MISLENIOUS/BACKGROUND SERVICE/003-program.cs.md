

[New]() | [Old]

# Program.cs (Complete Worker Service Example)

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

var builder = Host.CreateApplicationBuilder(args);

//
// -----------------------------------------------------
// Configuration
// -----------------------------------------------------
//
// Automatically loads:
// - appsettings.json
// - appsettings.{Environment}.json
// - Environment Variables
// - Command-line Arguments
//

//
// -----------------------------------------------------
// Run as Windows Service
// -----------------------------------------------------
//

builder.Services.AddWindowsService(options =>
{
    options.ServiceName = "Employee Worker Service";
});

//
// -----------------------------------------------------
// Run as Linux systemd Service
// -----------------------------------------------------
//

builder.Services.AddSystemd();

//
// -----------------------------------------------------
// Logging
// -----------------------------------------------------
//

// builder.Logging.ClearProviders();

// builder.Logging.AddConsole();

// builder.Logging.AddDebug();

//
// -----------------------------------------------------
// Dependency Injection (DI)
// -----------------------------------------------------
//

// Background Worker
builder.Services.AddHostedService<Worker>();

// Singleton Service
// builder.Services.AddSingleton<IMailService, MailService>();

// Scoped Service
// builder.Services.AddScoped<IEmployeeService, EmployeeService>();

// Transient Service
// builder.Services.AddTransient<IReportService, ReportService>();

// HttpClient
// builder.Services.AddHttpClient();

// Entity Framework Core
// builder.Services.AddDbContext<AppDbContext>(options =>
//     options.UseSqlServer(
//         builder.Configuration.GetConnectionString("DefaultConnection")));

// Options Pattern
// builder.Services.Configure<AppSettings>(
//     builder.Configuration.GetSection("AppSettings"));

//
// -----------------------------------------------------
// Build Host
// -----------------------------------------------------
//

var host = builder.Build();

//
// -----------------------------------------------------
// Run Host
// -----------------------------------------------------
//

host.Run();
```

---

# What Each Section Does

## `using Microsoft.Extensions.DependencyInjection;`

Provides Dependency Injection (DI).

Used for:

- `AddHostedService()`
- `AddSingleton()`
- `AddScoped()`
- `AddTransient()`
- `AddHttpClient()`

---

## `using Microsoft.Extensions.Hosting;`

Provides hosting features.

Includes:

- `Host`
- `BackgroundService`
- `IHostedService`
- `HostApplicationBuilder`

---

## `using Microsoft.Extensions.Logging;`

Adds logging support.

Example:

```csharp
builder.Logging.AddConsole();
```

---

# Create Host

```csharp
var builder = Host.CreateApplicationBuilder(args);
```

Creates the Worker Service host.

Automatically configures:

- Dependency Injection
- Logging
- Configuration
- Environment
- appsettings.json
- appsettings.{Environment}.json
- Environment Variables
- Command-line Arguments

---

# Configuration

The following are loaded automatically:

- `appsettings.json`
- `appsettings.Development.json`
- `appsettings.Production.json`
- Environment Variables
- Command-line Arguments

Access values with:

```csharp
builder.Configuration["Key"];

builder.Configuration.GetConnectionString("DefaultConnection");
```

---

# Windows Service

```csharp
builder.Services.AddWindowsService(options =>
{
    options.ServiceName = "Employee Worker Service";
});
```

Allows the Worker Service to run as a **Windows Service**.

If deployed as a Windows Service:

```
services.msc
```

will show

```
Employee Worker Service
```

instead of the executable name.

---

# Linux Service

```csharp
builder.Services.AddSystemd();
```

Allows the Worker Service to run under **Linux systemd**.

Examples:

- Ubuntu
- Debian
- Rocky Linux
- CentOS
- RHEL

---

# Logging

```csharp
builder.Logging.ClearProviders();
```

Removes default logging providers.

---

```csharp
builder.Logging.AddConsole();
```

Writes logs to the console.

---

```csharp
builder.Logging.AddDebug();
```

Writes logs to Visual Studio Debug Output.

---

# Register Background Service

```csharp
builder.Services.AddHostedService<Worker>();
```

Registers the `Worker` class.

When the application starts:

- Creates one `Worker`
- Calls `ExecuteAsync()`
- Runs until the application stops

---

# Register Other Services

Singleton

```csharp
builder.Services.AddSingleton<IMailService, MailService>();
```

One instance for the application's lifetime.

---

Scoped

```csharp
builder.Services.AddScoped<IEmployeeService, EmployeeService>();
```

One instance per scope (commonly used in Web APIs).

---

Transient

```csharp
builder.Services.AddTransient<IReportService, ReportService>();
```

Creates a new instance every time it is requested.

---

HttpClient

```csharp
builder.Services.AddHttpClient();
```

Registers `HttpClient` for calling external APIs.

---

Entity Framework Core

```csharp
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")));
```

Registers EF Core with SQL Server.

---

Options Pattern

```csharp
builder.Services.Configure<AppSettings>(
    builder.Configuration.GetSection("AppSettings"));
```

Binds configuration values to a C# class.

---

# Build Host

```csharp
var host = builder.Build();
```

Creates the application host.

After this:

- Services are created.
- Logging is ready.
- Configuration is ready.
- Hosted services are ready.

---

# Run Host

```csharp
host.Run();
```

Starts the Worker Service.

This:

- Starts the host.
- Starts `Worker.ExecuteAsync()`.
- Keeps the application running.
- Stops gracefully when the application exits.

---

# Complete Execution Flow

```text
Application Starts
        │
        ▼
Host.CreateApplicationBuilder()
        │
        ├── Load appsettings.json
        ├── Load Environment Variables
        ├── Configure Logging
        ├── Configure DI
        └── Detect Environment
        │
        ▼
Register Services
        │
        ├── AddWindowsService()
        ├── AddSystemd()
        ├── AddHostedService<Worker>()
        ├── AddSingleton()
        ├── AddScoped()
        ├── AddTransient()
        ├── AddHttpClient()
        └── AddDbContext()
        │
        ▼
Build()
        │
        ▼
Run()
        │
        ▼
Worker.ExecuteAsync()
        │
        ▼
Background Task Runs
        │
        ▼
Application Stops
        │
        ▼
CancellationToken Triggered
        │
        ▼
Worker Stops Gracefully
        │
        ▼
Host Stops
```




## Old Structure:

# Program.cs (Old Style - Program Class) for Worker Service (.NET 5 and Earlier)

```csharp
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.Extensions.Logging;

namespace EmployeeWorkerService
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateHostBuilder(args).Build().Run();
        }

        public static IHostBuilder CreateHostBuilder(string[] args)
        {
            return Host.CreateDefaultBuilder(args)

                // Run as Windows Service
                .UseWindowsService()

                // Run as Linux systemd Service
                .UseSystemd()

                // Configure Logging
                .ConfigureLogging(logging =>
                {
                    logging.ClearProviders();

                    logging.AddConsole();

                    logging.AddDebug();
                })

                // Register Services
                .ConfigureServices((hostContext, services) =>
                {
                    // Register Background Worker
                    services.AddHostedService<Worker>();

                    // Register Singleton Service
                    // services.AddSingleton<IMailService, MailService>();

                    // Register Scoped Service
                    // services.AddScoped<IEmployeeService, EmployeeService>();

                    // Register Transient Service
                    // services.AddTransient<IReportService, ReportService>();

                    // Register HttpClient
                    // services.AddHttpClient();

                    // Register Entity Framework Core
                    // services.AddDbContext<AppDbContext>(options =>
                    //     options.UseSqlServer(
                    //         hostContext.Configuration.GetConnectionString("DefaultConnection")));

                    // Register Options Pattern
                    // services.Configure<AppSettings>(
                    //     hostContext.Configuration.GetSection("AppSettings"));
                });
        }
    }
}
```

---

# Explanation

## `Main()`

```csharp
public static void Main(string[] args)
{
    CreateHostBuilder(args).Build().Run();
}
```

Application entry point.

Execution order:

```
Main()
    ↓
CreateHostBuilder()
    ↓
Build()
    ↓
Run()
```

---

## `CreateHostBuilder()`

```csharp
public static IHostBuilder CreateHostBuilder(string[] args)
```

Creates and configures the Generic Host.

Returns an `IHostBuilder`.

---

## `Host.CreateDefaultBuilder(args)`

Creates the default host and automatically configures:

- Dependency Injection (DI)
- Configuration
- Logging
- Environment
- appsettings.json
- appsettings.{Environment}.json
- Environment Variables
- Command-line Arguments

---

## `.UseWindowsService()`

```csharp
.UseWindowsService()
```

Allows the Worker Service to run as a **Windows Service**.

Use this when deploying on Windows Server.

---

## `.UseSystemd()`

```csharp
.UseSystemd()
```

Allows the Worker Service to integrate with **Linux systemd**.

Use this when deploying on Linux.

---

## `.ConfigureLogging()`

```csharp
.ConfigureLogging(logging =>
{
    logging.ClearProviders();

    logging.AddConsole();

    logging.AddDebug();
})
```

Configures logging.

### `ClearProviders()`

Removes default logging providers.

### `AddConsole()`

Writes logs to the console.

### `AddDebug()`

Writes logs to the Visual Studio Debug Output window.

---

## `.ConfigureServices()`

```csharp
.ConfigureServices((hostContext, services) =>
{
})
```

Registers all services for Dependency Injection (DI).

---

## `AddHostedService<Worker>()`

```csharp
services.AddHostedService<Worker>();
```

Registers the background worker.

When the application starts:

- Creates one `Worker`
- Calls `ExecuteAsync()`
- Keeps it running until shutdown

---

## `AddSingleton()`

```csharp
services.AddSingleton<IMailService, MailService>();
```

One instance for the entire application lifetime.

---

## `AddScoped()`

```csharp
services.AddScoped<IEmployeeService, EmployeeService>();
```

One instance per scope.

Mostly used in ASP.NET Core Web APIs.

---

## `AddTransient()`

```csharp
services.AddTransient<IReportService, ReportService>();
```

Creates a new instance every time it is requested.

---

## `AddHttpClient()`

```csharp
services.AddHttpClient();
```

Registers `HttpClient` for calling external APIs.

---

## `AddDbContext()`

```csharp
services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        hostContext.Configuration.GetConnectionString("DefaultConnection")));
```

Registers Entity Framework Core with SQL Server.

---

## `Build()`

```csharp
.Build()
```

Builds the application host.

Creates:

- DI Container
- Logging
- Configuration
- Hosted Services

---

## `Run()`

```csharp
.Run();
```

Starts the host.

This:

- Starts all hosted services.
- Calls `Worker.ExecuteAsync()`.
- Keeps the application running.
- Stops gracefully on shutdown.

---

# Complete Execution Flow

```text
Program Starts
        │
        ▼
Main()
        │
        ▼
CreateHostBuilder()
        │
        ▼
Host.CreateDefaultBuilder()
        │
        ├── Load appsettings.json
        ├── Load appsettings.{Environment}.json
        ├── Load Environment Variables
        ├── Configure Logging
        ├── Configure DI
        └── Detect Environment
        │
        ▼
UseWindowsService()
        │
        ▼
UseSystemd()
        │
        ▼
ConfigureLogging()
        │
        ▼
ConfigureServices()
        │
        ├── AddHostedService()
        ├── AddSingleton()
        ├── AddScoped()
        ├── AddTransient()
        ├── AddHttpClient()
        └── AddDbContext()
        │
        ▼
Build()
        │
        ▼
Run()
        │
        ▼
Worker.ExecuteAsync()
        │
        ▼
Background Task Running...
        │
        ▼
Application Stops
        │
        ▼
CancellationToken Triggered
        │
        ▼
Worker Stops Gracefully
        │
        ▼
Host Stops
```

# New vs Old Style

| Feature | New Style (.NET 6+) | Old Style (.NET 5 and Earlier) |
|---------|----------------------|--------------------------------|
| Entry point | Top-level statements | `Main()` method |
| Host creation | `Host.CreateApplicationBuilder()` | `Host.CreateDefaultBuilder()` |
| Windows Service | `AddWindowsService()` | `UseWindowsService()` |
| Linux Service | `AddSystemd()` | `UseSystemd()` |
| Register Worker | `AddHostedService<Worker>()` | `AddHostedService<Worker>()` |
| Build | `builder.Build()` | `.Build()` |
| Run | `host.Run()` | `.Run()` |
| Recommended | ✅ .NET 6+ | Legacy projects (.NET 5 and earlier) |