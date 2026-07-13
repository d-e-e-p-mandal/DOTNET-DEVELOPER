
## Method 3 : Using IOptions : Recomended

### What is IOptions?

- `IOptions<T>` binds configuration to a strongly typed class.
- Recommended approach in ASP.NET Core.

**Simple Meaning:**
- Configuration Object Binding

**File Name:** `appsettings.json`
```json
{
  "ApiSettings": {
    "BaseUrl": "https://api.company.com",
    "ApiKey": "12345"
  }
}
```
### Project Structure:
```text
Project
│
├── Helper or Configurations
│   └── ApiSettings.cs //create class here of configuration
├── Services
├── Controllers
├── appsettings.json
└── Program.cs
```

### Create Settings Class:
```cs
public class ApiSettings
{
    public string BaseUrl { get; set; }
    public string ApiKey { get; set; }
}
```
⸻

### Register In: **`Program.cs`**
```cs
builder.Services.Configure<ApiSettings>( builder.Configuration.GetSection("ApiSettings"));
```
⸻

### Inject IOptions:
```cs
using Microsoft.Extensions.Options;
public class EmployeeService
{
    private readonly ApiSettings _settings;
    public EmployeeService(IOptions<ApiSettings> options)
    {
        _settings = options.Value;
    }
}
```

### Usage:
```cs
string apiKey = _settings.ApiKey;
string url = _settings.BaseUrl;
```

**Flow:**
```text
appsettings.json
        ↓
ApiSettings Section
        ↓
Configure<ApiSettings>()
        ↓
IOptions<ApiSettings>
        ↓
ApiSettings Object

⸻

Comparison

Method	Usage
IConfiguration	Read Values Directly
Helper + IConfiguration	Centralized Configuration Logic
IOptions	Strongly Typed Configuration

⸻

Which One Is Preferred?

Small Project
      ↓
IConfiguration
Medium Project
      ↓
Helper + IConfiguration
Large Project
      ↓
IOptions<T>

⸻

Quick Revision

Configuration
      ↓
appsettings.json
Method 1
      ↓
IConfiguration
_configuration["ApiSettings:ApiKey"]
Method 2
      ↓
Helper Class
      ↓
GetSection()
      ↓
Get<T>()
Method 3
      ↓
IOptions<T>
Configure<T>()
      ↓
Strongly Typed Settings
Most Recommended
      ↓
IOptions<T>
```