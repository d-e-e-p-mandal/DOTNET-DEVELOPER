# Configuration

# What is Configuration?
- Configuration means storing application settings.
- Configuration is used to store application settings outside the source code.

**Used for:**
- Connection strings
- API keys
- Environment settings
- Application settings


**Examples:**
- Connection Strings
- API URLs
- API Keys
- JWT Settings
- SMTP Settings
- SFTP Settings


**Usually stored in:**
```text
appsettings.json
```

**Simple Meaning:** Configuration = Application Settings


**ASP.NET Core Configuration Files:**
- appsettings.json
- appsettings.Development.json
- appsettings.Production.json
- Custom defined

**File Location:**

```text
Project
│
├── appsettings.json
├── appsettings.Development.json
├── appsettings.Production.json
```


### 1. appsettings.json
- Main configuration file of ASP.NET Core.

**Stores:**
- Common settings
- Database connection
- API settings


### Example

```json
{
  "ConnectionStrings": {
    "DefaultConnection":
    "Server=.;Database=TestDb;Trusted_Connection=True;"
  },

  "AppSettings": {
    "AppName": "MyApp"
  }
}
```

**Explanation:**

**ConnectionStrings:**

- Stores database connection strings.


**DefaultConnection:**
- Connection name.

**AppSettings:**
- Custom application settings.


**AppName:**
- AppName is custom and it value also custom set.
- Custom setting value.


**Purpose:**

Used for:
- Database settings
- API settings
- Global settings

---

### Environment Flow

```text
Application Starts
        ↓
Load appsettings.json
        ↓
Check Environment
        ↓
        ↓Override Settings / if exisit
        ↓
Load appsettings.Development.json / Production

```

---
