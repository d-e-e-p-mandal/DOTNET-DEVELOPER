
[program.cs] [startup.cs]

# OLD ARCHITECTURE (.NET CORE 3.1 / .NET 5)

Old ASP.NET Core architecture used:

```text
Program.cs + Startup.cs
```

Both files worked together.

---

# COMPLETE FLOW

```text
Program.cs
      ↓
Create Host
      ↓
Load Startup.cs
      ↓
ConfigureServices()
      ↓
Dependency Injection
      ↓
Configure()
      ↓
Middleware Pipeline
      ↓
Routing
      ↓
Controllers
      ↓
Response
```

---

# 1. Program.cs

---

# PURPOSE OF Program.cs

`Program.cs` is the main entry point of application.

Application execution starts from here.

---

# RESPONSIBILITIES OF Program.cs

- Start application
- Create Host
- Configure Kestrel
- Configure IIS
- Load Startup.cs
- Build application
- Run application

---

# FULL OLD Program.cs CODE

```cs
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Hosting;

namespace MyProject
{
    public class Program
    {
        // Main Entry Point
        public static void Main(string[] args)
        {
            CreateHostBuilder(args).Build().Run();
        }

        // Create Host Builder
        public static IHostBuilder CreateHostBuilder(string[] args) =>

            Host.CreateDefaultBuilder(args)

                // Configure Web Host
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    // Load Startup.cs
                    webBuilder.UseStartup<Startup>();
                });
    }
}
```

---

# STEP-BY-STEP EXPLANATION

---

# using Microsoft.AspNetCore.Hosting;

## Purpose

Used for:
- Web hosting
- Kestrel configuration
- IIS integration

---

# using Microsoft.Extensions.Hosting;

## Purpose

Used for:
- Generic Host
- Application hosting

---

# Program Class

```cs
public class Program
```

## Purpose

Main application class.

---

# Main Method

```cs
public static void Main(string[] args)
```

## Purpose

Application starts here.

CLR executes Main() first.

---

# Flow

```text
Application Starts
       ↓
Main()
       ↓
CreateHostBuilder()
```

---

# CreateHostBuilder()

```cs
CreateHostBuilder(args)
```

## Purpose

Creates application host.

---

# IHostBuilder

```cs
IHostBuilder
```

## Purpose

Used to configure:
- Server
- Logging
- Configuration
- Dependency Injection

---

# Flow

```text
IHostBuilder
      ↓
Configure Application
      ↓
Build()
      ↓
IHost
```

---

# Host.CreateDefaultBuilder()

```cs
Host.CreateDefaultBuilder(args)
```

## Purpose

Creates default ASP.NET Core host.

---

# Automatically Configures

- Kestrel Server
- IIS Integration
- Logging
- Configuration
- Dependency Injection
- appsettings.json
- Environment Variables

---

# Internal Flow

```text
CreateDefaultBuilder()
        ↓
Load appsettings.json
        ↓
Load Environment Variables
        ↓
Configure Logging
        ↓
Configure Kestrel
        ↓
Configure DI
```

---

# ConfigureWebHostDefaults()

```cs
.ConfigureWebHostDefaults()
```

## Purpose

Adds default web configurations.

---

# Configures

- Kestrel Server
- IIS Integration
- Routing
- Hosting

---

# webBuilder

```cs
webBuilder
```

## Purpose

Used for web server configuration.

---

# UseStartup<Startup>()

```cs
webBuilder.UseStartup<Startup>();
```

## Purpose

Loads Startup.cs.

Tells ASP.NET Core:

```text
Use Startup.cs for application configuration
```

---

# Build()

```cs
.Build()
```

## Purpose

Builds application.

Creates final host.

---

# Before Build()

```text
Only configuration exists
```

---

# After Build()

```text
Application ready to run
```

---

# Run()

```cs
.Run()
```

## Purpose

Starts Kestrel server.

Application begins listening for requests.

---

# COMPLETE FLOW OF Program.cs

```text
Main()
    ↓
CreateHostBuilder()
    ↓
CreateDefaultBuilder()
    ↓
ConfigureWebHostDefaults()
    ↓
UseStartup<Startup>()
    ↓
Build()
    ↓
Run()
```

---

# SIMPLE MEANING

```text
Program.cs = Application Starter
```

---

# 2. Startup.cs

---

# PURPOSE OF Startup.cs

`Startup.cs` is the main configuration file.

Used to:
- Register services
- Configure middleware
- Configure routing
- Configure authentication

---

# RESPONSIBILITIES OF Startup.cs

- Configure Dependency Injection
- Configure Middleware Pipeline
- Configure Authentication
- Configure Authorization
- Configure Routing
- Configure Swagger
- Configure CORS

---

# FULL Startup.cs CODE

```cs
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
using Microsoft.Extensions.Hosting;
using Microsoft.EntityFrameworkCore;

namespace MyProject
{
    public class Startup
    {
        // IConfiguration
        public IConfiguration Configuration { get; }

        // Constructor
        public Startup(IConfiguration configuration)
        {
            Configuration = configuration;
        }

        // Configure Services
        public void ConfigureServices(IServiceCollection services)
        {
            // Add Controllers
            services.AddControllers();

            // Add MVC
            services.AddControllersWithViews();

            // Add Razor Pages
            services.AddRazorPages();

            // Add DbContext
            services.AddDbContext<AppDbContext>(options =>
                options.UseSqlServer(
                    Configuration.GetConnectionString("DefaultConnection")
                ));

            // Add Swagger
            services.AddSwaggerGen();

            // Add CORS
            services.AddCors();

            // Add Session
            services.AddSession();

            // Add Memory Cache
            services.AddMemoryCache();

            // Add Authentication
            services.AddAuthentication();

            // Add Authorization
            services.AddAuthorization();

            // Add HttpClient
            services.AddHttpClient();

            // Dependency Injection
            services.AddScoped<IEmployeeService, EmployeeService>();

            services.AddTransient<IProductService, ProductService>();

            services.AddSingleton<ICacheService, CacheService>();
        }

        // Configure Middleware Pipeline
        public void Configure(IApplicationBuilder app,
                              IWebHostEnvironment env)
        {
            // Development Environment
            if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();

                app.UseSwagger();

                app.UseSwaggerUI();
            }

            // Security
            app.UseHsts();

            // HTTPS
            app.UseHttpsRedirection();

            // Static Files
            app.UseStaticFiles();

            // Routing
            app.UseRouting();

            // CORS
            app.UseCors(policy =>
                policy.AllowAnyOrigin()
                      .AllowAnyHeader()
                      .AllowAnyMethod());

            // Authentication
            app.UseAuthentication();

            // Authorization
            app.UseAuthorization();

            // Session
            app.UseSession();

            // Custom Middleware
            app.UseMiddleware<ExceptionMiddleware>();

            // Endpoints
            app.UseEndpoints(endpoints =>
            {
                endpoints.MapControllers();

                endpoints.MapRazorPages();
            });
        }
    }
}
```

---

# STEP-BY-STEP EXPLANATION

---

# IConfiguration

```cs
public IConfiguration Configuration { get; }
```

## Purpose

Access configuration values.

Reads:
- appsettings.json
- Environment Variables

---

# Constructor

```cs
public Startup(IConfiguration configuration)
{
    Configuration = configuration;
}
```

## Purpose

Inject configuration object.

---

# ConfigureServices()

```cs
public void ConfigureServices(IServiceCollection services)
```

## Purpose

Registers services into Dependency Injection container.

---

# Common Services

| Service | Purpose |
|---|---|
| AddControllers | API Controllers |
| AddDbContext | Database |
| AddSwaggerGen | Swagger |
| AddCors | Cross-Origin Requests |
| AddAuthentication | Authentication |
| AddAuthorization | Authorization |
| AddSession | Sessions |
| AddMemoryCache | Caching |

---

# Dependency Injection

```cs
services.AddScoped<IEmployeeService, EmployeeService>();
```

## Purpose

Register custom services.

---

# DI Lifetimes

| Lifetime | Meaning |
|---|---|
| AddTransient | New object every time |
| AddScoped | One object per request |
| AddSingleton | One object entire app |

---

# Configure()

```cs
public void Configure(IApplicationBuilder app,
                      IWebHostEnvironment env)
```

## Purpose

Configures middleware pipeline.

---

# IWebHostEnvironment

```cs
env
```

## Purpose

Gets current environment.

Examples:
- Development
- Production
- Staging

---

# IsDevelopment()

```cs
env.IsDevelopment()
```

## Purpose

Checks if application is running in Development mode.

---

# UseDeveloperExceptionPage()

```cs
app.UseDeveloperExceptionPage();
```

## Purpose

Shows detailed errors in development.

---

# UseSwagger()

```cs
app.UseSwagger();
```

## Purpose

Generates Swagger JSON.

---

# UseSwaggerUI()

```cs
app.UseSwaggerUI();
```

## Purpose

Opens Swagger UI.

---

# UseHsts()

```cs
app.UseHsts();
```

## Purpose

Enforces HTTPS security.

---

# UseHttpsRedirection()

```cs
app.UseHttpsRedirection();
```

## Purpose

Redirects:
- HTTP → HTTPS

---

# UseStaticFiles()

```cs
app.UseStaticFiles();
```

## Purpose

Enables:
- CSS
- JS
- Images

---

# UseRouting()

```cs
app.UseRouting();
```

## Purpose

Enables endpoint routing.

---

# UseCors()

```cs
app.UseCors();
```

## Purpose

Allows frontend access.

---

# UseAuthentication()

```cs
app.UseAuthentication();
```

## Purpose

Validates user identity.

---

# UseAuthorization()

```cs
app.UseAuthorization();
```

## Purpose

Checks user permissions.

---

# UseSession()

```cs
app.UseSession();
```

## Purpose

Enables sessions.

---

# UseMiddleware()

```cs
app.UseMiddleware<ExceptionMiddleware>();
```

## Purpose

Adds custom middleware.

---

# UseEndpoints()

```cs
app.UseEndpoints()
```

## Purpose

Maps endpoints.

---

# MapControllers()

```cs
endpoints.MapControllers();
```

## Purpose

Maps API controllers.

---

# MapRazorPages()

```cs
endpoints.MapRazorPages();
```

## Purpose

Maps Razor Pages.

---

# COMPLETE FLOW OF Startup.cs

```text
Startup.cs Loaded
        ↓
ConfigureServices()
        ↓
Register Services
        ↓
Configure()
        ↓
Configure Middleware
        ↓
Routing
        ↓
Controllers
        ↓
Response
```

---

# COMPLETE OLD ARCHITECTURE FLOW

```text
Browser Request
       ↓
Kestrel Server
       ↓
Program.cs
       ↓
Startup.cs
       ↓
ConfigureServices()
       ↓
Dependency Injection
       ↓
Configure()
       ↓
Middleware Pipeline
       ↓
Routing
       ↓
Controller
       ↓
Service
       ↓
Repository
       ↓
Database
       ↓
Response
```

---

# OLD vs NEW ARCHITECTURE

| OLD | NEW |
|---|---|
| Program.cs + Startup.cs | Only Program.cs |
| More boilerplate | Minimal hosting |
| Separate ConfigureServices | Inside Program.cs |
| Separate Configure | Inside Program.cs |

---

# SIMPLE REAL-LIFE ANALOGY

| ASP.NET Core Part | Real Life |
|---|---|
| Program.cs | Factory opening manager |
| Startup.cs | Factory setup manager |
| ConfigureServices | Hiring workers |
| Configure | Setting security/routing |
| Middleware | Security checkpoints |
| Kestrel | Main factory gate |