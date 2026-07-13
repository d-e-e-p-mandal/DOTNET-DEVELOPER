# C# .NET `.csproj` File:

- `.csproj` stands for: C# Project File
- Every .NET project contains one `.csproj` file.

**Example:**
- EmployeeApi.csproj
- BankingApp.csproj
- WorkerService.csproj

---

**Purpose:**

The `.csproj` file tells .NET:
- How To Build Project
- Which Framework To Use
- Which Packages To Install
- Which Files To Include
- Project Settings

**Example:** Project Structure:

```text
EmployeeApi
│
├── Controllers
├── Models
├── Services
├── Program.cs
├── appsettings.json
│
└── EmployeeApi.csproj
```


### Basic .csproj File

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
  <PropertyGroup>
    <TargetFramework>
      net8.0
    </TargetFramework>
  </PropertyGroup>
</Project>
```


### Project
- Root element.

```xml
<Project>
</Project>
```

**Contains:**

- Entire Project Configuration


### Sdk

**Purpose:**
- Specifies project type.

**Example:**
```xml
<Project Sdk="Microsoft.NET.Sdk">
```

**Meaning:**
- Console Application
- Class Library


```xml
<Project Sdk="Microsoft.NET.Sdk.Web">
```

**Meaning:**
- ASP.NET Core Web API
- MVC
- Razor Pages


### PropertyGroup

**Purpose:**
- Contains project settings.

**Example:**

```xml
<PropertyGroup>

</PropertyGroup>
```

---

### TargetFramework

**Purpose:**
- Specifies .NET version.

**Example:**
```xml
<TargetFramework>
    net8.0
</TargetFramework>
```

**Meaning:** .NET 8


**Common Values:**
- net6.0
- net7.0
- net8.0
- net9.0

## OutputType

**Purpose:**
- Defines output type.

**Example:**
```xml
<OutputType>
    Exe
</OutputType>
```

**Meaning:** Console Application

**Values:**
- Exe
- Library
- WinExe


### Nullable

**Purpose:**
- Enable Nullable Reference Types.

**Example:**
```xml
<Nullable>
    enable
</Nullable>
```

**Meaning:**
- String Can Be Null Checked


**Example:**
```cs
string? name;
```


### ImplicitUsings

**Purpose:**
- Automatically imports common namespaces.

**Example:**
```xml
<ImplicitUsings>
    enable
</ImplicitUsings>
```

**Without:**
```cs
using System;
using System.Collections.Generic;
```

**With:** Automatically Available


### RootNamespace

**Purpose:**
- Default namespace.

**Example:**
```xml
<RootNamespace>
    EmployeeApi
</RootNamespace>
```


### AssemblyName

**Purpose:**
- Output DLL name.

**Example:**
```xml
<AssemblyName>
    EmployeeApi
</AssemblyName>
```

**Output:**
```text
EmployeeApi.dll
```


### Version

**Purpose:** Application Version.

**Example:**
```xml
<Version>
    1.0.0
</Version>
```

### Authors

**Purpose:**
- Project Author.

**Example:**
```xml
<Authors>
    Deep
</Authors>
```


### Company

**Purpose:**
- Company Name.

**Example:**
```xml
<Company>
    ABC Ltd
</Company>
```

### Description

**Purpose:** Project Description.

**Example:**
```xml
<Description>
    Employee Management API
</Description>
```


### PackageReference

**Purpose:** Install NuGet Packages.

**Example:**
```xml
<ItemGroup>
  <PackageReference
      Include="Serilog.AspNetCore"
      Version="9.0.0" />
</ItemGroup>
```

**Meaning:**
- Install Package
- Restore Package
- Use Package


### Multiple Packages
```xml
<ItemGroup>
  <PackageReference
      Include="Serilog.AspNetCore"
      Version="9.0.0" />
  <PackageReference
      Include="Microsoft.EntityFrameworkCore"
      Version="9.0.0" />
</ItemGroup>
```

### ProjectReference

**Purpose:**
- Reference Another Project.

**Example:**
```xml
<ItemGroup>
  <ProjectReference
      Include="..\Core\Core.csproj" />
</ItemGroup>
```

**Meaning:**
```text
API Project
      ↓
Uses Core Project
```

**Folder Structure Example:**
```text
Solution
│
├── API
│     └── API.csproj
│
├── Core
│     └── Core.csproj
│
└── Infrastructure
      └── Infrastructure.csproj
```


### Content

**Purpose:**
- Include Files.

**Example:**
```xml
<ItemGroup>
  <Content
      Include="Files\*.txt" />
</ItemGroup>
```


### None

**Purpose:**
- Keep file without compilation.

**Example:**
```xml
<ItemGroup>
  <None
      Include="Sample.txt" />
</ItemGroup>
```


### EmbeddedResource

**Purpose:**
- Embed file inside assembly.

**Example:**
```xml
<ItemGroup>
  <EmbeddedResource
      Include="Templates\Email.html" />
</ItemGroup>
```


### User Secrets

**Purpose** Store local secrets.

**Example:**
```xml
<UserSecretsId>
    abc123
</UserSecretsId>
```

**Used For:**
- API Keys
- Passwords
- Connection Strings


### Generate Documentation
```xml
<GenerateDocumentationFile>
    true
</GenerateDocumentationFile>
```

**Purpose:**
- Generate XML Documentation


### LangVersion

**Purpose:** Specify C# Version.

**Example:**
```xml
<LangVersion>
    latest
</LangVersion>
```


### RuntimeIdentifier

**Purpose:**
- Target Specific OS.

**Example:**
```xml
<RuntimeIdentifier>
    win-x64
</RuntimeIdentifier>
```

**Examples:**
- win-x64
- linux-x64
- osx-arm64


### Self Contained Deployment

```xml
<SelfContained>
    true
</SelfContained>
```

**Meaning:**
- Include .NET Runtime


### PublishSingleFile

```xml
<PublishSingleFile>
    true
</PublishSingleFile>
```

Meaning:

```text
Generate Single EXE
```

---

### CopyToOutputDirectory

**Example:**
```xml
<Content Include="appsettings.json">
  <CopyToOutputDirectory>
      Always
  </CopyToOutputDirectory>
</Content>
```

**Purpose:**
Copy File To Bin Folder



### ASP.NET Core Web API csproj

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>

    <TargetFramework>
        net8.0
    </TargetFramework>

    <Nullable>
        enable
    </Nullable>

    <ImplicitUsings>
        enable
    </ImplicitUsings>

  </PropertyGroup>

  <ItemGroup>

    <PackageReference
        Include="Microsoft.EntityFrameworkCore"
        Version="9.0.0" />

    <PackageReference
        Include="Serilog.AspNetCore"
        Version="9.0.0" />

  </ItemGroup>

</Project>
```

---

# Common Sections

```text
Project
      ↓
Root Element

Sdk
      ↓
Project Type

PropertyGroup
      ↓
Settings

ItemGroup
      ↓
Packages
      ↓
References
      ↓
Files
```

---

# Most Important Elements

```xml
<Project>

<PropertyGroup>

<TargetFramework>

<Nullable>

<ImplicitUsings>

<ItemGroup>

<PackageReference>

<ProjectReference>
```

---

# Build Flow

```text
.csproj
      ↓
dotnet restore
      ↓
Download Packages
      ↓
dotnet build
      ↓
Compile Code
      ↓
DLL / EXE Created
```