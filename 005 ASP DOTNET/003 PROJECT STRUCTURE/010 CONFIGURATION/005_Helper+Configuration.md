## Method 2 : Helper Class + IConfiguration

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

### Read Using Helper Class:
```cs
public class ConfigHelper
{
    private readonly IConfiguration _configuration;
    
    public ConfigHelper(IConfiguration configuration)
    {
        _configuration = configuration;
    }
    public ApiSettings GetApiSettings()
    {
        return _configuration.GetSection("ApiSettings").Get<ApiSettings>();
    }
}
```

**Usage**
```cs
var settings = helper.GetApiSettings();
string apiKey = settings.ApiKey;
```

**Flow:**
```text
appsettings.json
        ↓
IConfiguration
        ↓
ConfigHelper
        ↓
ApiSettings Object
```