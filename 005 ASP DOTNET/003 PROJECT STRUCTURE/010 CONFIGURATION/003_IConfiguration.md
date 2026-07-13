## Method 1 : Using IConfiguration

### What is IConfiguration?s
- IConfiguration is used to read configuration values directly.

**Namespace:**
```cs
using Microsoft.Extensions.Configuration;
```
⸻

**Constructor Injection:**
```cs
public class EmployeeService
{
    private readonly IConfiguration _configuration;
    public EmployeeService(IConfiguration configuration)
    {
        _configuration = configuration;
    }
}
```

**Read Single Value:**
```cs
string apiKey = _configuration["ApiSettings:ApiKey"];
```
**Result:** 12345

**Read Connection String:**
```cs
string connectionString = _configuration.GetConnectionString("DefaultConnection");
```

**Read Section Value:**
```cs
string url = _configuration["ApiSettings:BaseUrl"];
```
**Result:** `https://api.company.com`

**Flow:**
```
appsettings.json
        ↓
IConfiguration
        ↓
Read Value
```