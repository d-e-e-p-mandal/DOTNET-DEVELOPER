
## 1. Download .NET SDK

**Go to official site:**
	•	Microsoft .NET

**Steps:**
	1.	Open browser
	2.	Search: “.NET SDK download”
	3.	Choose Latest LTS version (Recommended)
	4.	Select macOS (Apple Silicon / Intel based on your Mac)
	5.	Download .pkg installer


**Install .NET SDK:**
	1.	Open downloaded .pkg file
	2.	Click Continue → Install
	3.	Enter Mac password
	4.	Finish installation

✔️ That’s it — SDK is installed


*Verify Installation:*

Open Terminal and run:
```bash
dotnet --version
```
- If installed correctly → you will see version like:
```
8.0.xxx
```


**Check All Details:**
```bash
dotnet --info
```
This shows:
	•	SDK version
	•	Runtime version
	•	Installed paths




## Dotnet Hosting:

[Download Hosting version]()

### Hosting: Version 8.0.0
```bash
dotnet add package Microsoft.Extensions.Hosting --version 8.0.0
```

File: `.csproj`
```cs
<PackageReference Include="Microsoft.Extensions.Hosting" Version="8.0.0" />
```