## 2. Microsoft.EntityFrameworkCore.SqlServer

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

*Purpose:*
- SQL Server Provider
- Required for:SQL Server Database Connection


## Using OnConfiguring : (Old System)

Program.cs:
```cs
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    protected override void OnConfiguring(DbContextOptionsBuilder options)
    {
        options.UseSqlServer(
            "Server=.;Database=TestDB;Trusted_Connection=True;"
        );
    }
}
```



## Using DataAccessContext Folder (Most Used, Best Practice)

```text
MyProject/
├── DataAccessContext/
│   └── AppDbContext.cs
```

```cs
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
    public AppDbContext(DbContextOptions<AppDbContext> options): base(options) {}

    public DbSet<Employee> Employees { get; set; }
}
```

```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=.;Database=TestDB;Trusted_Connection=True;"
  }
}
```

**File :** Program.cs
```cs
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")
    ));
```

```cs
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
```

Key Points:
	•	Keep connection string in appsettings.json
	•	Improves security & flexibility
	•	Avoid hardcoding
