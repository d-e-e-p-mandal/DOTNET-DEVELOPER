
# What is Installation?

Entity Framework Core works using NuGet packages.

Packages provide:
- Database providers
- Migrations
- ORM features

---

# NuGet Package Installation

## 1. Microsoft.EntityFrameworkCore
- Core EF Functionality

```bash
dotnet add package Microsoft.EntityFrameworkCore
```



# 2. Microsoft.EntityFrameworkCore.Tools
- Required for`Add-Migration Update-Database`

```bash
dotnet add package Microsoft.EntityFrameworkCore.Tools
```


# 3. Microsoft.EntityFrameworkCore.Design

```bash
dotnet add package Microsoft.EntityFrameworkCore.Design
```

**Purpose:**
- Design Time Services

**Required for:**
- Migrations
- Scaffolding

---

# Install EF CLI Tool

```bash
dotnet tool install --global dotnet-ef
```

# Verify Installation

```bash
dotnet ef
```

# List Installed Tools

```bash
dotnet tool list -g
```