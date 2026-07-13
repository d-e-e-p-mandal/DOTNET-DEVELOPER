# MVC Structure:
```text
MyProject/
│
├── Controllers/
│   ├── EmployeeController.cs
│   └── ProductController.cs
│
├── Models/
│   ├── Employee.cs
│   └── Product.cs
│
├── Data/
│   └── AppDbContext.cs
│
├── DependencyInjection/     → Service registration (DI setup)
│    └── ServiceExtensions.cs → AddScoped / AddTransient / AddSingleton
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
├── DTOs/
│   ├── EmployeeDTO.cs
│   └── ProductDTO.cs
│
├── Middleware/
│   ├── ExceptionMiddleware.cs
│   └── JwtMiddleware.cs
│
├── Helpers/
│   ├── JwtHelper.cs
│   ├── FileHelper.cs
│   └── EmailHelper.cs
│
├── Mappings/
│   └── AutoMapperProfile.cs
│
├── Configurations/
│   ├── JwtSettings.cs
│   └── EmailSettings.cs
│
├── Migrations/
│   ├── InitialCreate.cs
│   └── AppDbContextModelSnapshot.cs
│
├── Views/
│   ├── Home/
│   │   └── Index.cshtml
│   │
│   └── Shared/
│       └── _Layout.cshtml
│
├── wwwroot/
│   ├── css/
│   ├── js/
│   ├── images/
│   └── uploads/
│
├── Properties/
│   └── launchSettings.json
│
├── appsettings.json
│
├── appsettings.Development.json
│
├── appsettings.Production.json
│
├── Program.cs
│
├── MyProject.csproj
│
├── README.md
│
└── .gitignore
```