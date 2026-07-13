
# DbContext: (Internal Details)

DbContext is the main class of Entity Framework Core
- It is used to interact with the database
- It acts as a bridge between your application and database


**Comes From:**
```cs
Microsoft.EntityFrameworkCore
```
**Namespace:**
```cs
using Microsoft.EntityFrameworkCore;
```
**Basic Syntax:**
```cs
using Microsoft.EntityFrameworkCore;

public class AppDbContext : DbContext
{
	// Constructor : 
	public AppDbContext(DbContextOptions<AppDbContext> options) : base(options) {} 

    public DbSet<Employee> Employees { get; set; }
}
```

**Options:** Options carries the database connection information and sends it to the superclass (DbContext). It is predefined in .NET to configure the database automatically.
```cs
builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseSqlServer(
        builder.Configuration.GetConnectionString("DefaultConnection")
    ));
```

- Similar configaruation .cs file in dotnet
```cs
private readonly IConfiguration _configuration;
public AppSettings(IConfiguration configuration)
{
    _configuration = configuration;
}
```

Table :
```cs
[Table("TableName")]
public class Employee
{
    public int Id { get; set; }
    public string Name { get; set; }
}
```

DbContext -> Base class (EF Core)
AppDbContext -> Your custom context
DbSet<Employee> -> Represents table

Meaning:
	•	Employees → Table
	•	Employee → Structure


Constructor :
Without constructor - Older versions allowed it, but now:  
- Required for proper configuration  
- Needed for DI



------------------------------------


# DbContext : Internal Implement

## Class : DbContext
```cs
using System;
using System.Threading;
using System.Threading.Tasks;

public class DbContext : IDisposable
{
    // Options (configuration like connection string)
    protected DbContextOptions Options { get; }

    // Constructor
    public DbContext(DbContextOptions options)
    {
        Options = options;
    }

    // Represents tables
    public DbSet<TEntity> Set<TEntity>() where TEntity : class
    {
        // Returns a DbSet for the given entity
        return new DbSet<TEntity>();
    }

    // Save changes (sync)
    public virtual int SaveChanges()
    {
        // Detect changes
        ChangeTracker.DetectChanges();

        // Save to database (simplified)
        Console.WriteLine("Changes saved to database");

        return 1;
    }

    // Save changes (async)
    public virtual async Task<int> SaveChangesAsync(CancellationToken cancellationToken = default)
    {
        ChangeTracker.DetectChanges();

        // Simulate async DB operation
        await Task.Delay(100);

        Console.WriteLine("Changes saved asynchronously");

        return 1;
    }

    // Change tracking
    public ChangeTracker ChangeTracker { get; } = new ChangeTracker();

    // Dispose (cleanup)
    public void Dispose()
    {
        Console.WriteLine("DbContext disposed");
    }
}
```

class : DbContextOptions
```cs
public class DbContextOptions
{
    // Connection string (database info)
    public string ConnectionString { get; set; }

    // Database provider (SQL Server, MySQL, etc.)
    public string Provider { get; set; }

    // Enable logging
    public bool EnableLogging { get; set; }

    // Constructor
    public DbContextOptions(string connectionString, string provider)
    {
        ConnectionString = connectionString;
        Provider = provider;
    }
}
```


### What is IDisposable?

- IDisposable is an interface in .NET
- Used to release resources manually

Definition :  
It provides a method to clean up unmanaged resources like files, database connections, memory, etc.


Interface Definition
```cs
public interface IDisposable
{
    void Dispose();
}
```
- Only one method: Dispose()


Why do we need it?
- Some resources are NOT managed by garbage collector:
	•	Database connections
	•	File handles
	•	Network connections

- So we must release them manually

Example Without IDisposable 
```cs
var connection = new SqlConnection("conn");
connection.Open();
```
- If not closed → memory/resource leak

Example With IDisposable
```cs
using (var connection = new SqlConnection("conn"))
{
    connection.Open();
}
```
 
**Internally : using works ONLY with IDisposable**
```cs
var connection = new SqlConnection("conn");
try
{
    connection.Open();
}
finally
{
    if (connection != null)
    {
        connection.Dispose(); // compiler added this
    }
}
```

Automatically calls : connection.Dispose();

---

Custom Class Example
```cs
public class MyResource : IDisposable
{
    public void Dispose()
    {
        Console.WriteLine("Resources released");
    }
}
```

How DbContext Uses It : DbContext implements IDisposable:
```cs
public class DbContext : IDisposable
{
    public void Dispose()
    {
        // close DB connection
    }
}
```

Internal Flow
```
Create object
     ↓
Use resource
     ↓
Dispose() called
     ↓
Resource released
```
