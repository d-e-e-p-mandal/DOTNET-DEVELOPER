# Program.cs :

```cs
using Microsoft.EntityFrameworkCore;

// Create builder
var builder = WebApplication.CreateBuilder(args);

// Add services to DI container

// 1. Add Controllers
builder.Services.AddControllers();

// 2. Add DbContext
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")
    ));

// 3. Add Custom Services (Extension Method)
builder.Services.AddApplicationServices();

// Build app
var app = builder.Build();

// Middleware pipeline

app.UseHttpsRedirection();

app.UseAuthorization();

// Map Controllers
app.MapControllers();

// Run application
app.Run();
```

------

## Program.cs (More Functionality) :
```cs
using Microsoft.EntityFrameworkCore;

var builder = WebApplication.CreateBuilder(args);

// Add services

// 1. Add Controllers + JSON Options
builder.Services.AddControllers()
    .AddJsonOptions(options =>
    {
        // Example settings
        options.JsonSerializerOptions.PropertyNamingPolicy = null; // keep PascalCase
        options.JsonSerializerOptions.WriteIndented = true;        // pretty JSON
    });

// 2. Add DbContext
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")
    ));

// 3. Add Custom Services
builder.Services.AddApplicationServices();

// Build app
var app = builder.Build();


// Create Scope (for DB seeding / initialization)
using (var scope = app.Services.CreateScope())
{
    var services = scope.ServiceProvider;

    try
    {
        var db = services.GetRequiredService<AppDbContext>();

        // Example: ensure DB created
        db.Database.EnsureCreated();

        // OR you can call:
        // DbSeeder.Seed(db);
    }
    catch (Exception ex)
    {
        Console.WriteLine(ex.Message);
    }
}


// Middleware pipeline
app.UseHttpsRedirection();

app.UseAuthorization();

// Map controllers
app.MapControllers();

// Run app
app.Run();
```