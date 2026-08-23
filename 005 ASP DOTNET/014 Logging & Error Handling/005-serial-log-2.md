dotnet add package Serilog.Extensions.Logging
<PackageReference Include="Serilog.Extensions.Logging" Version="10.0.0" />

dotnet add package Serilog
dotnet add package Serilog.Sinks.Console
dotnet add package Serilog.Sinks.File
dotnet add package Serilog.Settings.Configuration


<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Serilog.AspNetCore" Version="..." />
    <PackageReference Include="Serilog.Sinks.Console" Version="..." />
    <PackageReference Include="Serilog.Sinks.File" Version="..." />
    <PackageReference Include="Serilog.Settings.Configuration" Version="..." />
  </ItemGroup>

</Project>


cs
 Log.Logger = new LoggerConfiguration()
     .MinimumLevel.Information()
     .WriteTo.Console()
     .WriteTo.File(
         Path.Combine(AppContext.BaseDirectory, "Logs", "log-.txt"),
         rollingInterval: RollingInterval.Day,
         fileSizeLimitBytes: 10 * 1024 * 1024,
         rollOnFileSizeLimit: true,
         retainedFileCountLimit: 30,
         shared: true,
         flushToDiskInterval: TimeSpan.FromSeconds(1))
     .CreateLogger();

    builder.Logging.ClearProviders(); // disable default console
    builder.Logging.AddSerilog(Log.Logger);




//Replace default logging providers
//builder.Logging.ClearProviders();
builder.Logging.AddSerilog();
//builder.Logging.AddSerilog(Log.Logger);



------------
1.builder.Logging.AddSerilog(Log.Logger);  // create instance
2.builder.Logging.AddSerilog();  //global use
The first is implicit; the second is explicit.












---------------
old:

using System;
using System.IO;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Logging;
using Serilog;

namespace UCO_NACH_ADD_USER
{
    public class Program
    {
        public static void Main(string[] args)
        {
            string logPath = Path.Combine(Directory.GetCurrentDirectory(), "_Logs/");
            if (!Directory.Exists(logPath))
                Directory.CreateDirectory(logPath);

            // Configure Serilog for the File only
            Log.Logger = new LoggerConfiguration()
                .MinimumLevel.Information()
                .WriteTo.File(
                    Path.Combine(logPath, "log-.txt"),
                    rollingInterval: RollingInterval.Day,
                    retainedFileCountLimit: 30
                )
                .CreateLogger();

            try
            {
                Log.Information("Starting host worker service...");

                var host = CreateHostBuilder(args).Build();
                host.Run();
            }
            catch (Exception ex)
            {
                Log.Fatal(ex, "Host terminated unexpectedly");
            }
            finally
            {
                Log.CloseAndFlush();
            }
        }

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureLogging(logging =>
                {
                 
                    logging.ClearProviders();
                    logging.AddConsole(); 
                    
      
                    logging.AddSerilog(Log.Logger, dispose: true); 
                })
                .ConfigureServices((hostContext, services) =>
                {
                    IConfiguration configuration = hostContext.Configuration;

                    services.AddHostedService<Worker>();
                    services.AddDbContext<DataAccessContext>(options => 
                        options.UseOracle(configuration.GetConnectionString("OrclConStr")));
                })
                .UseWindowsService();
    }
}



-------------

========

## Serilog File Logging — .NET 8

1. Required Packages

Main Serilog packages
```bash
dotnet add package Serilog
dotnet add package Serilog.AspNetCore
dotnet add package Serilog.Sinks.Console
dotnet add package Serilog.Sinks.File
dotnet add package Serilog.Settings.Configuration
```

**.csproj:**
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>net8.0</TargetFramework>
    <Nullable>enable</Nullable>
    <ImplicitUsings>enable</ImplicitUsings>
  </PropertyGroup>
  <ItemGroup>
    <PackageReference Include="Serilog.AspNetCore" Version="..." />
    <PackageReference Include="Serilog.Sinks.Console" Version="..." />
    <PackageReference Include="Serilog.Sinks.File" Version="..." />
    <PackageReference Include="Serilog.Settings.Configuration" Version="..." />
  </ItemGroup>
</Project>


2. Configure Serilog

```cs
Log.Logger = new LoggerConfiguration()
    .MinimumLevel.Information()
    .WriteTo.Console()
    .WriteTo.File(
        Path.Combine(
            AppContext.BaseDirectory,
            "Logs",
            "log-.txt"),
        rollingInterval: RollingInterval.Day,
        fileSizeLimitBytes: 10 * 1024 * 1024,
        rollOnFileSizeLimit: true,
        retainedFileCountLimit: 30,
        shared: true,
        flushToDiskInterval: TimeSpan.FromSeconds(1))
    .CreateLogger();
```
**File location:**
```
Application / Publish Folder
│
├── MyApplication.dll
├── appsettings.json
└── Logs
    ├── log-2026...txt
    ├── log-2026...txt
    └── ...
```
AppContext.BaseDirectory points to the application’s base/publish location.


3. Connect Serilog with .NET Logging

### Option 1:
```bash
builder.Logging.ClearProviders();
builder.Logging.AddSerilog(Log.Logger);
```
Here you explicitly give the existing Log.Logger instance to the .NET logging system.
```
Log.Logger
    ↓
AddSerilog(Log.Logger)
    ↓
.NET ILogger
    ↓
Serilog
    ↓
Console + File
```
### Option 2:

```cs
builder.Logging.AddSerilog();
```
This uses the global Log.Logger that you have already configured.
```
Log.Logger
    ↓
AddSerilog()
    ↓
.NET ILogger
    ↓
Serilog
```
Important

These are alternatives:
```cs
builder.Logging.AddSerilog(Log.Logger);
```
or:
```cs
builder.Logging.AddSerilog();
```
You normally do not need both.

⸻

### 4. ClearProviders()

builder.Logging.ClearProviders();

Removes the logging providers that were already configured by the default host.

For example:
```
Before ClearProviders()
.NET Logging
    │
    ├── Console
    ├── Debug
    └── EventSource
```
After:

builder.Logging.ClearProviders();
builder.Logging.AddSerilog();

Conceptually:
```
.NET Logging
    │
    └── Serilog
          ├── Console
          └── File
```
Because your Serilog configuration contains:

.WriteTo.Console()
.WriteTo.File(...)

⸻

5. Old Structure — Program.cs

Your existing old structure can remain like this:
```cs
using System;
using System.IO;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.EntityFrameworkCore;
using Microsoft.Extensions.Logging;
using Serilog;
namespace UCO_NACH_ADD_USER
{
    public class Program
    {
        public static void Main(string[] args)
        {
            string logPath = Path.Combine(
                Directory.GetCurrentDirectory(),
                "_Logs/");
            if (!Directory.Exists(logPath))
                Directory.CreateDirectory(logPath);
            // Configure Serilog for the File only
            Log.Logger = new LoggerConfiguration()
                .MinimumLevel.Information()
                .WriteTo.File(
                    Path.Combine(logPath, "log-.txt"),
                    rollingInterval: RollingInterval.Day,
                    retainedFileCountLimit: 30
                )
                .CreateLogger();
            try
            {
                Log.Information("Starting host worker service...");
                var host = CreateHostBuilder(args).Build();
                host.Run();
            }
            catch (Exception ex)
            {
                Log.Fatal(ex, "Host terminated unexpectedly");
            }
            finally
            {
                Log.CloseAndFlush();
            }
        }
        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureLogging(logging =>
                {
                    logging.ClearProviders();
                    logging.AddConsole();
                    logging.AddSerilog(
                        Log.Logger,
                        dispose: true);
                })
                .ConfigureServices((hostContext, services) =>
                {
                    IConfiguration configuration =
                        hostContext.Configuration;
                    services.AddHostedService<Worker>();
                    services.AddDbContext<DataAccessContext>(
                        options =>
                            options.UseOracle(
                                configuration.GetConnectionString(
                                    "OrclConStr")));
                })
                .UseWindowsService();
    }
}
```
⸻

6. Old Structure Flow
```
Program.Main()
      ↓
Create Logs folder
      ↓
Create Serilog LoggerConfiguration
      ↓
Log.Logger
      ↓
CreateHostBuilder()
      ↓
ConfigureLogging()
      ↓
ClearProviders()
      ↓
AddConsole()
      ↓
AddSerilog(Log.Logger)
      ↓
Worker + DbContext
      ↓
UseWindowsService()
      ↓
host.Run()
```
⸻

7. What Log.Logger Means

This:
```cs
Log.Logger = new LoggerConfiguration()
    .MinimumLevel.Information()
    .WriteTo.File(...)
    .CreateLogger();
```
creates the global Serilog logger.

Then:

Log.Information("Application started");

can directly use that global logger.

For example:
```cs
Log.Information("Application started");
Log.Error(ex, "Something went wrong");
```
⸻

8. What ILogger<T> Does

Your application code normally uses Microsoft’s ILogger<T>:
```cs
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;
    public Worker(ILogger<Worker> logger)
    {
        _logger = logger;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _logger.LogInformation("Worker started.");
        await Task.CompletedTask;
    }
}
```
Flow:
```
Worker
  ↓
ILogger<Worker>
  ↓
Microsoft Logging
  ↓
Serilog Provider
  ↓
Serilog
  ↓
File / Console
```
⸻

9. AddSerilog(Log.Logger) vs AddSerilog()

Explicit logger

builder.Logging.AddSerilog(Log.Logger);

You explicitly say:

Use this particular Log.Logger instance.

Global logger

builder.Logging.AddSerilog();

You say:

Use the global Log.Logger.

So the simple memory rule is:

AddSerilog(Log.Logger)
        ↓
Explicitly provide the logger
AddSerilog()
        ↓
Use global Log.Logger

⸻

10. Serilog.Extensions.Logging vs Serilog.AspNetCore

For a modern ASP.NET Core application, Serilog.AspNetCore is the commonly used integration package.

dotnet add package Serilog.AspNetCore

It integrates Serilog with ASP.NET Core’s ILogger infrastructure.

Serilog itself is the core logging library:

Serilog
   ↓
LoggerConfiguration
   ↓
Log.Logger

Sinks decide where logs go:

Serilog
   │
   ├── Serilog.Sinks.Console
   │       ↓
   │    Console
   │
   └── Serilog.Sinks.File
           ↓
        Log File

Important package distinction

You generally don’t need to add Serilog.Extensions.Logging separately when Serilog.AspNetCore already provides the ASP.NET Core integration you need. For your .NET 8 ASP.NET Core application, the simpler package set is:

Serilog
Serilog.AspNetCore
Serilog.Sinks.Console
Serilog.Sinks.File
Serilog.Settings.Configuration   ← only if configuring Serilog through appsettings.json

This keeps the setup cleaner.