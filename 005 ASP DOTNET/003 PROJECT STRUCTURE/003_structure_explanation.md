# .NET WEB API PROJECT STRUCTURE

```text
MyWebApi/
│
├── Controllers/
├── Models/
├── DTOs/
├── Data/
├── Repositories/
├── Services/
├── Middleware/
├── Helpers/
├── Configurations/
├── Mappings/
├── Extensions/
├── Migrations/
├── Properties/
├── wwwroot/
│
├── appsettings.json
├── appsettings.Development.json
├── appsettings.Production.json
│
├── Program.cs
├── MyWebApi.csproj
├── README.md
└── .gitignore
```

---

# 1. Controllers Folder

```text
Controllers/
```

## Purpose

Handles API requests.

## Example

```text
EmployeeController.cs
ProductController.cs
```

## Simple Meaning

```text
Controller = Request handler
```

---

# 2. Models Folder

```text
Models/
```

## Purpose

Represents database tables/entities.

## Example

```text
Employee.cs
Product.cs
```

## Simple Meaning

```text
Model = Data structure
```

---

# 3. DTOs Folder

```text
DTOs/
```

## Purpose

Transfers data between client and server.

## Example

```text
EmployeeDTO.cs
CreateEmployeeDTO.cs
UpdateEmployeeDTO.cs
```

## Simple Meaning

```text
DTO = Data transfer object
```

---

# 4. Data Folder

```text
Data/
```

## Purpose

Contains DbContext and database connection.

## Example

```text
AppDbContext.cs
```

## Simple Meaning

```text
Data = Database connection layer
```

---

# 5. Repositories Folder

```text
Repositories/
```

## Purpose

Handles database queries.

## Example

```text
EmployeeRepository.cs
ProductRepository.cs
```

## Simple Meaning

```text
Repository = Database operation layer
```

---

# 6. Services Folder

```text
Services/
```

## Purpose

Contains business logic.

## Example

```text
EmployeeService.cs
ProductService.cs
```

## Simple Meaning

```text
Service = Business logic layer
```

---

# 7. Middleware Folder

```text
Middleware/
```

## Purpose

Handles request and response pipeline.

## Example

```text
ExceptionMiddleware.cs
JwtMiddleware.cs
```

## Simple Meaning

```text
Middleware = Request checker
```

---

# 8. Helpers Folder

```text
Helpers/
```

## Purpose

Contains helper/utility classes.

## Example

```text
JwtHelper.cs
FileHelper.cs
PasswordHelper.cs
```

## Simple Meaning

```text
Helpers = Common reusable methods
```

---

# 9. Configurations Folder

```text
Configurations/
```

## Purpose

Stores strongly typed settings classes.

## Example

```text
JwtSettings.cs
SwaggerSettings.cs
```

## Simple Meaning

```text
Configurations = Settings classes
```

---

# 10. Mappings Folder

```text
Mappings/
```

## Purpose

Contains AutoMapper configuration.

## Example

```text
AutoMapperProfile.cs
```

## Simple Meaning

```text
Mappings = Object mapping configuration
```

---

# 11. Extensions Folder

```text
Extensions/
```

## Purpose

Contains extension methods.

## Example

```text
ServiceExtensions.cs
```

## Simple Meaning

```text
Extensions = Custom extra methods
```

---

# 12. Migrations Folder

```text
Migrations/
```

## Purpose

Stores Entity Framework migration files.

## Example

```text
InitialCreate.cs
```

## Simple Meaning

```text
Migrations = Database history/version
```

---

# 13. Properties Folder

```text
Properties/
```

## Purpose

Contains launch settings.

## Example

```text
launchSettings.json
```

## Simple Meaning

```text
Properties = Project launch configuration
```

---

# 14. wwwroot Folder

```text
wwwroot/
```

## Purpose

Stores static files.

## Contains

```text
css/
js/
images/
uploads/
```

## Simple Meaning

```text
wwwroot = Public static files
```

---

# 15. appsettings.json

## Purpose

Stores common application settings.

## Example

```json
{
  "ConnectionStrings": {
    "DefaultConnection":
    "Server=.;Database=TestDb;"
  }
}
```

## Simple Meaning

```text
appsettings.json = Main configuration file
```

---

# 16. appsettings.Development.json

## Purpose

Development environment settings.

## Simple Meaning

```text
Development-only configuration
```

---

# 17. appsettings.Production.json

## Purpose

Production/live server settings.

## Simple Meaning

```text
Production environment configuration
```

---

# 18. Program.cs

## Purpose

Main entry point of application.

Starts and configures Web API.

## Example

```csharp
var builder = WebApplication.CreateBuilder(args);

var app = builder.Build();

app.Run();
```

## Simple Meaning

```text
Program.cs = Application starter
```

---

# 19. MyWebApi.csproj

## Purpose

Project configuration file.

## Stores

- .NET version
- Package references

## Simple Meaning

```text
.csproj = Project information file
```

---

# 20. README.md

## Purpose

Project documentation.

## Simple Meaning

```text
README.md = Project guide/documentation
```

---

# 21. .gitignore

## Purpose

Ignores unnecessary files from Git.

## Example

```text
bin/
obj/
```

## Simple Meaning

```text
.gitignore = Files not uploaded to GitHub
```

---

# SIMPLE WEB API FLOW

```text
Client Request
      ↓
Controller
      ↓
Service
      ↓
Repository
      ↓
DbContext
      ↓
Database
      ↓
JSON Response
```

---

# SIMPLE RESPONSIBILITY TABLE

| Folder/File | Responsibility |
|---|---|
| Controllers | Handle requests |
| Models | Data structure |
| DTOs | Transfer data |
| Data | Database connection |
| Repositories | Database queries |
| Services | Business logic |
| Middleware | Request pipeline |
| Helpers | Utility methods |
| Configurations | Settings classes |
| Mappings | Object mapping |
| Extensions | Extra methods |
| Migrations | Database history |
| wwwroot | Static files |
| Program.cs | Start app |
| appsettings.json | Configuration |
| .csproj | Project configuration |