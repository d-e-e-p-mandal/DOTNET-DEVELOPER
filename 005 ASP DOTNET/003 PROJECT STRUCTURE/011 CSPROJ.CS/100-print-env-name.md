## Need to fix not working now:


## PrintName : 
```xml
<Target Name="PrintEnvironmentFile" BeforeTargets="Publish">

  <PropertyGroup>
    <EnvFileName Condition="'$(EnvironmentName)' != ''">
      appsettings.$(EnvironmentName).json
    </EnvFileName>

    <EnvFileName Condition="'$(EnvironmentName)' == ''">
      NO ENVIRONMENT PROVIDED
    </EnvFileName>
  </PropertyGroup>

  <Message Importance="High" Text="=============================================" />
  <Message Importance="High" Text="PUBLISH APPSETTINGS FILE" />
  <Message Importance="High" Text="Environment : $(EnvironmentName)" />
  <Message Importance="High" Text="File        : $(EnvFileName)" />
  <Message Importance="High" Text="=============================================" />

</Target>
```





```xml
<Project Sdk="Microsoft.NET.Web">
    <PropertyGroup>
        <TargetFramework> net8.0</TargetFramwork>
    </PropertyGroup>

    <!-- When Environment Name passed -->
    <Target Name="PrintEnvironment" BeforeTargets="Build;Publish">
      <Message
        Condition=" '$(EnvironmentName)' !=''"
        Importance ="hign"
        Text="Building with Environment: $(EnvironmentName)"/>

      <Message
        Condition="'$(EnvironmentName)' !=''"
        Importance="high"
         Text="Using File: appsettings.$(EnvironmentName).json"/>
    
    <!-- When EnvironmentName is not passed -->
      <Message
        Condition="'$(EnvironmentName)' ==''"
        Importance="high"
        Text="No EnvironmentName specific"/>
    
      <Message
        Condition="'$(EnvironmentName)' ==''"
        Importance="high"
        Text="Using File: appsettings.$(EnvironmentName).json"/>
    </Target>

    <ItemGroup>
      <None Update="**\appsettings*.json">
        <CopyToOutputDirectory>
      </None>
    </ItemGroup>
</Project>
```


### Output Examples:
**Without specifying an evironment:**
```bash
dotnet build
```

**Output:**
- No environmentName specified
- Using default application configuration (appsettings.json).

**With Production:**
```bash
dotnet build -p:EnvironmentName=Production
```

**Output:**
- Building with Environment: Production
- Using file: appsettings.Production.json

