# Web API structure:

### Full Structure:
```
MyWebApi/
│
├── Controllers/
│   ├── EmployeeController.cs
│   └── ProductController.cs
│
├── Models/
│   ├── Employee.cs
│   └── Product.cs
│
├── DTOs/
│   ├── EmployeeDTO.cs
│   ├── CreateEmployeeDTO.cs
│   └── UpdateEmployeeDTO.cs
│
├── DataAccessContext/
│   └── AppDbContext.cs
│
├── Repositories/
│   ├── Interfaces and Implementation Together in one file 
│   OR
│   ├── Interfaces/
│   │   ├── IEmployeeRepository.cs
│   │   └── IProductRepository.cs
│   │
│   ├── EmployeeRepository.cs
│   └── ProductRepository.cs
│
├── Services/
│   ├── Interfaces and Implementation Together in one file 
│   OR
│   ├── Interfaces/
│   │   ├── IEmployeeService.cs
│   │   └── IProductService.cs
│   │
│   ├── EmployeeService.cs
│   └── ProductService.cs
│
├── Middleware/
│   ├── ExceptionMiddleware.cs
│   └── JwtMiddleware.cs
│
├── Helpers/
│   ├── JwtHelper.cs
│   ├── PasswordHelper.cs
│   └── FileHelper.cs
│
├── Configurations/
│   ├── JwtSettings.cs
│   └── SwaggerSettings.cs
│
├── Mappings/
│   └── AutoMapperProfile.cs
│
├── Extensions/
│   └── ServiceExtensions.cs
│
├── Migrations/
│   ├── InitialCreate.cs
│   └── AppDbContextModelSnapshot.cs
│
├── Properties/
│   └── launchSettings.json
│
├── wwwroot/
│
├── appsettings.json
│
├── appsettings.Development.json
│
├── appsettings.Production.json
│
├── Program.cs
│
├── MyWebApi.csproj
│
├── README.md
│
└── .gitignore
```


#### My structure with SQL/LINQ: (Simple Version)
```
MyApi/
│
├── Controllers/              → Handles HTTP requests (API endpoints)
│
├── Models/                  → Entity classes (DB tables structure) / Optional for raw SQL
│
├── Data/                    → Database related files
│    └── AppDbContext.cs     → DbContext (database connection)
│
├── DependencyInjection/     → Service registration (DI setup)
│    └── ServiceExtensions.cs → AddScoped / AddTransient / AddSingleton
├── DTOs/                    → Data Transfer Objects (request/response models)
│
├── Services/                
│    ├── Interfaces and Implementation Together in one file 
│    OR
│    ├── Interfaces/         → Service interfaces
│    └── Implementations/    → Service implementations
│
├── Repository/              → Business logic layer
│    ├── Interfaces and Implementation Together in one file 
│    OR
│    ├── Interfaces/         → Repository interfaces
│    └── Implementations/    → Repository implementations
│
├── Query/                   → Linq Query stroed here as functional / IQueryable or SQL(Procedure) (Optional(Better Approach): Direct store id db and execute Procedure)
│
├── Program.cs               → Application entry point
│
├── appsettings.json         → Main configuration (DB, JWT, etc.)
├── appsettings.Development.json → Development-specific config
│
└── Properties/
     └── launchSettings.json → Run/debug settings
```