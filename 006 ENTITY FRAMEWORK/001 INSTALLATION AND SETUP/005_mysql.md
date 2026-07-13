## 2. Microsoft.EntityFrameworkCore.SqlServer

```bash
dotnet add package Microsoft.EntityFrameworkCore.SqlServer
```

*Purpose:*
- SQL Server Provider
- Required for:SQL Server Database Connection


## DbContext:

### Method 1 : Open directly when need to access (Not recomended to use)

```cs
string connectionString = "Server=.;Database=YourDB;Trusted_Connection=True;";
        using (SqlConnection con = new SqlConnection(connectionString))
        {
            con.Open(); // open connection
            string query = "SELECT Id, Name FROM Students";
            SqlCommand cmd = new SqlCommand(query, con);
            SqlDataReader reader = cmd.ExecuteReader();
            while (reader.Read())
            {
                Console.WriteLine(reader["Id"] + " " + reader["Name"]);
            }
        }
```


## Method 2: (Best Use)

**File:** Program.cs
```cs
using Microsoft.EntityFrameworkCore;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddDbContext<AppDbContext>(options =>
    options.UseMySql(
        builder.Configuration.GetConnectionString("DefaultConnection"),
        ServerVersion.AutoDetect(builder.Configuration.GetConnectionString("DefaultConnection"))
    ));

var app = builder.Build();

app.Run();
```
appsetting.json
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "server=localhost;database=testdb;user=root;password=1234;"
  }
}
```