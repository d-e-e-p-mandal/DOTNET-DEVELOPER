# .NET FULL COMMAND SYLLABUS

---

# 🟢 1. .NET CLI BASICS

```bash
dotnet --version
dotnet --info
dotnet help
dotnet --help
dotnet --list-sdks
dotnet --list-runtimes
```

---

# 🟡 2. PROJECT CREATION COMMANDS

## Create Projects

```bash
dotnet new
dotnet new console
dotnet new classlib
dotnet new web
dotnet new webapi
dotnet new mvc
dotnet new razor
dotnet new worker
dotnet new grpc
dotnet new angular
dotnet new react
dotnet new blazor
dotnet new blazorserver
dotnet new blazorwasm
dotnet new xunit
dotnet new nunit
dotnet new mstest
```

## Create Solution

```bash
dotnet new sln
```

## Create Git Ignore

```bash
dotnet new gitignore
```

## Create Editor Config

```bash
dotnet new editorconfig
```

## Create Global JSON

```bash
dotnet new globaljson
```

## Create With Name

```bash
dotnet new console -n ProjectName
```

## Create In Specific Folder

```bash
dotnet new webapi -o MyFolder
```

---

# 🔵 3. SOLUTION COMMANDS

```bash
dotnet sln add
dotnet sln remove
dotnet sln list
```

---

# 🟣 4. BUILD COMMANDS

```bash
dotnet build
dotnet build -c Release
dotnet build -c Debug
dotnet clean
dotnet restore
dotnet msbuild
```

---

# 🟠 5. RUN COMMANDS

## Basic Run

```bash
dotnet run
dotnet run --project
```

## Run Modes

```bash
dotnet run -c Release
dotnet run -c Debug
```

## Run With URL

```bash
dotnet run --urls
dotnet run --urls=http://localhost:5000
dotnet run --urls=https://localhost:5001
```

## Run With Environment

```bash
dotnet run --environment Development
dotnet run --environment Production
dotnet run --environment Staging
```

## Run With Framework

```bash
dotnet run --framework net8.0
dotnet run --framework net7.0
```

## Run Options

```bash
dotnet run --no-build
dotnet run --no-restore
dotnet run --launch-profile
```

## Run With Arguments

```bash
dotnet run arg1 arg2
```

---

# 🔴 6. WATCH & HOT RELOAD COMMANDS

```bash
dotnet watch
dotnet watch run
dotnet watch build
dotnet watch test
```

---

# ⚫ 7. PACKAGE MANAGEMENT COMMANDS

## Add Package

```bash
dotnet add package
```

## Remove Package

```bash
dotnet remove package
```

## Add Reference

```bash
dotnet add reference
```

## Remove Reference

```bash
dotnet remove reference
```

## List Packages

```bash
dotnet list package
```

## Restore Packages

```bash
dotnet restore
```

## Outdated Packages

```bash
dotnet list package --outdated
```

---

# 🟤 8. ENTITY FRAMEWORK TOOL COMMANDS

## Install EF Tool

```bash
dotnet tool install --global dotnet-ef
```

## Update EF Tool

```bash
dotnet tool update --global dotnet-ef
```

## Uninstall EF Tool

```bash
dotnet tool uninstall --global dotnet-ef
```

## Restore Tools

```bash
dotnet tool restore
```

## List Tools

```bash
dotnet tool list -g
dotnet tool list --global
```

---

# 🟢 9. ENTITY FRAMEWORK MIGRATION COMMANDS

## Create Migration

```bash
dotnet ef migrations add MigrationName
```

## Remove Migration

```bash
dotnet ef migrations remove
```

## List Migrations

```bash
dotnet ef migrations list
```

## Generate Migration Script

```bash
dotnet ef migrations script
```

## Bundle Migration

```bash
dotnet ef migrations bundle
```

---

# 🟡 10. ENTITY FRAMEWORK DATABASE COMMANDS

## Update Database

```bash
dotnet ef database update
```

## Drop Database

```bash
dotnet ef database drop
```

## Update Specific Migration

```bash
dotnet ef database update MigrationName
```

## Update To Initial State

```bash
dotnet ef database update 0
```

---

# 🔵 11. DBCONTEXT COMMANDS

## List DbContext

```bash
dotnet ef dbcontext list
```

## DbContext Information

```bash
dotnet ef dbcontext info
```

## Reverse Engineering

```bash
dotnet ef dbcontext scaffold
```

## Optimize DbContext

```bash
dotnet ef dbcontext optimize
```

---

# 🟣 12. PUBLISH COMMANDS

## Publish Project

```bash
dotnet publish
```

## Publish Release

```bash
dotnet publish -c Release
```

## Publish Debug

```bash
dotnet publish -c Debug
```

## Publish To Folder

```bash
dotnet publish -o ./publish
```

## Self Contained Publish

```bash
dotnet publish --self-contained
```

## Runtime Publish

```bash
dotnet publish -r win-x64
dotnet publish -r linux-x64
dotnet publish -r osx-x64
```

## Single File Publish

```bash
dotnet publish -p:PublishSingleFile=true
```

---

# 🟠 13. TESTING COMMANDS

## Run Tests

```bash
dotnet test
```

## Create Test Projects

```bash
dotnet new xunit
dotnet new nunit
dotnet new mstest
```

## Filter Tests

```bash
dotnet test --filter
```

---

# 🔴 14. NUGET COMMANDS

## Add Source

```bash
dotnet nuget add source
```

## Remove Source

```bash
dotnet nuget remove source
```

## List Sources

```bash
dotnet nuget list source
```

## Disable Source

```bash
dotnet nuget disable source
```

## Enable Source

```bash
dotnet nuget enable source
```

## Push Package

```bash
dotnet nuget push
```

## Delete Package

```bash
dotnet nuget delete
```

---

# ⚫ 15. DLL COMMANDS

## Run DLL

```bash
dotnet ProjectName.dll
```

## Run Published DLL

```bash
dotnet ./publish/ProjectName.dll
```

---

# 🟤 16. HTTPS & TRUST COMMANDS

## Trust HTTPS Certificate

```bash
dotnet dev-certs https --trust
```

## Clean Certificates

```bash
dotnet dev-certs https --clean
```

## Export Certificate

```bash
dotnet dev-certs https -ep
```

## Check Certificates

```bash
dotnet dev-certs https --check
```

---

# 🟢 17. TEMPLATE COMMANDS

## List Templates

```bash
dotnet new list
```

## Search Templates

```bash
dotnet new search
```

## Install Template

```bash
dotnet new install
```

## Uninstall Template

```bash
dotnet new uninstall
```

## Update Templates

```bash
dotnet new update
```

---

# 🟡 18. FORMAT & CODE QUALITY COMMANDS

## Format Code

```bash
dotnet format
```

## Verify Formatting

```bash
dotnet format --verify-no-changes
```

---

# 🔵 19. WORKLOAD COMMANDS

## List Workloads

```bash
dotnet workload list
```

## Install Workload

```bash
dotnet workload install
```

## Uninstall Workload

```bash
dotnet workload uninstall
```

## Restore Workload

```bash
dotnet workload restore
```

## Update Workload

```bash
dotnet workload update
```

---

# 🟣 20. DIAGNOSTICS COMMANDS

```bash
dotnet trace
dotnet dump
dotnet counters
dotnet monitor
```

---

# 🟠 21. CACHE COMMANDS

## Clear NuGet Cache

```bash
dotnet nuget locals all --clear
```

## List Cache

```bash
dotnet nuget locals all --list
```

---

# 🔴 22. VERBOSE & LOGGING COMMANDS

```bash
dotnet run -v detailed
dotnet run -v minimal
dotnet run -v diagnostic
dotnet build -v detailed
```

---

# ⚫ 23. FILE & REFERENCE COMMANDS

## List References

```bash
dotnet list reference
```

## List Projects

```bash
dotnet sln list
```

---

# 🟤 24. IMPORTANT .NET TOPICS

- Build Process
- Restore Process
- Migration Process
- Database Update Process
- Publish Process
- Hot Reload
- Launch Profiles
- Environment Variables
- URL Binding
- Dependency Injection
- Middleware
- Kestrel Server
- IIS Hosting
- Configuration System
- Logging
- Authentication
- Authorization
- Swagger
- Routing
- Minimal API
- MVC Architecture
- Web API Architecture
- Repository Pattern
- Service Pattern
- DTO Pattern
- Entity Framework Core
- LINQ
- Async/Await
- Background Services
- Worker Services
- SignalR
- gRPC
- Docker Support
- Azure Deployment
- JWT Authentication
- Identity Framework
- CORS
- API Versioning
- Exception Handling
- Caching
- Session Management
- AutoMapper
- Fluent Validation
- Serilog
- Health Checks
- Rate Limiting