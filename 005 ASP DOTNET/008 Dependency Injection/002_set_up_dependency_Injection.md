
### Service Extension Dependency Injection List in another file :

file : ServiceExtensions.cs
```cs
public static class ServiceExtensions
{
    public static IServiceCollection AddApplicationServices(this IServiceCollection services) //[Extension Method [Ref :c# Method 005]]
    {
        // all DI write here : interface -> implementss
        services.AddScoped<IEmployeeService, EmployeeService>();

        return services;
    }
}
```
file : Program.cs

```cs
// Add Services
builder.Services.AddApplicationServices();
```

```cs
using Microsoft.EntityFrameworkCore;

var builder = WebApplication.CreateBuilder(args);

// Add DbContext
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

// Add Services
builder.Services.AddApplicationServices();

// Add Controllers
builder.Services.AddControllers();

var app = builder.Build();

// Middleware
app.UseHttpsRedirection();
app.UseAuthorization();

app.MapControllers();

app.Run();
```