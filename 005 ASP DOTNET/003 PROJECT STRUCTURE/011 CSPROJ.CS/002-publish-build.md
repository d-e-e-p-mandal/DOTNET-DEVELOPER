## Publish : Build : Specific Environment File:
- Used to see see which appsettings.*.cs are used.
- Used to create build of specific appsettings.


##### Cmd:
```bash
dotnet publish -c Release -o .\publish -p:EnvironmentName=Development
```

```bash
dotnet publish -c Release -o .\publish /p:EnvironmentName=Development
```


### If We Want only that env file with appsetting.csproj + <Selected>

**File:** `.csproj` : Add this content in project
```xml
<PropertyGroup>
  <EnableDefaultContentItems>true</EnableDefaultContentItems>
</PropertyGroup>

<ItemGroup>
  <!-- Remove all appsettings files from publish -->
  <Content Update="appsettings*.json">
    <CopyToPublishDirectory>Never</CopyToPublishDirectory>
  </Content>

  <!-- Copy only selected environment file -->
  <Content Update="appsettings.$(EnvironmentName).json">
    <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
    <CopyToPublishDirectory>PreserveNewest</CopyToPublishDirectory>
  </Content>
</ItemGroup>

```