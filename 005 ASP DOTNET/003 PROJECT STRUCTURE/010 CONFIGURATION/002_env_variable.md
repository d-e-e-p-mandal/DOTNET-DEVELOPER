
## ASP.NET CORE ENVIRONMENTS
ASP.NET Core uses environments to run application differently in different situations.

**TYPES OF ENVIRONMENTS:**
- Development
- Staging
- Production
- Can be Create Custom

### Development
Used during coding and development.

**Features:**
- Detailed errors
- Swagger enabled
- Debugging enabled

**Config File:** appsettings.Development.json

## Example
```cs
if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
}
```

**Simple Meaning**
Development = Coding Environment



### Staging
Used for testing before production.

**Features:**
- Production-like environment
- Final testing
- QA testing

**Config File:** appsettings.Staging.json

## Simple Meaning
Staging = Testing Environment


### Production
Used for live application.

**Features:**
- High security
- Better performance
- Real users access application

**Config File:** appsettings.Production.json

**Example:**
```cs
if (!app.Environment.IsDevelopment())
{
    app.UseHsts();
}
```

**Simple Meaning:**
```text
Production = Live Environment
```


## ENVIRONMENT VARIABLE
```text
ASPNETCORE_ENVIRONMENT
```


**File:** launchSettings.json Example
```json
{
  "profiles": {
    "MyProject": {
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```


#### CHECK ENVIRONMENT
**Development:**
```cs
app.Environment.IsDevelopment()
```

**Production:**
```cs
app.Environment.IsProduction()
```

**Staging:**
```cs
app.Environment.IsStaging()
```


---

## What are Configuration Sources?
- Configuration sources are places from where ASP.NET Core reads settings.
- Configuration Source = Place Where Settings Stored



**Common Configuration Sources:**
- appsettings.json
- Environment Variables
- Secret Manager


#### Environment Variables
Environment Variables are settings stored in:
- Operating System
- Server
- Docker
- Azure

**Purpose:**
Used for:
- Environment settings
- Secret values
- Production configuration

---

**File:** *launchSettings.json*
```json
{
  "profiles": {
    "MyApp": {
      "environmentVariables": {
        "ASPNETCORE_ENVIRONMENT": "Development"
      }
    }
  }
}
```

**Run Time Set From Cmd Line:**

**Windows**
```bash - cmd
set ASPNETCORE_ENVIRONMENT=Production
```

```powershell
$env:ASPNETCORE_ENVIRONMENT="Production"
```

**Mac/Linux**
```bash
export ASPNETCORE_ENVIRONMENT=Production
```

### Secret Manager: Described Lated
Avoid storing sensitive data inside:
- appsettings.json

**Secrets are:**
- NOT stored inside project
- NOT pushed to GitHub


**Simple Meaning:**
```text
Secret Manager
    ↓
Safe Storage For Sensitive Data
```

---
