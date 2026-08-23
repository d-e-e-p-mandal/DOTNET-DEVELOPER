Log File Location

1. AppContext.BaseDirectory

string logPath = Path.Combine(
    AppContext.BaseDirectory,
    "Logs",
    "log-.txt"
);

* Points to the application’s base directory.
* In a build/publish, this is generally the folder containing the application’s deployed files.

Example:

Publish
├── MyApp.dll
├── appsettings.json
└── Logs
    └── log-.txt

Typical location:

bin\Release\net8.0\publish\Logs\log-.txt

2. Directory.GetCurrentDirectory()

string logPath = Path.Combine(
    Directory.GetCurrentDirectory(),
    "_Logs",
    "log-.txt"
);

* Points to the current working directory from which the application is running.
* This can be different from the application’s DLL/publish location.

Example:

Current Working Directory
└── _Logs
    └── log-.txt

Simple Difference

AppContext.BaseDirectory
        ↓
Application / DLL / Publish location
Directory.GetCurrentDirectory()
        ↓
Current working location

For logs in the deployed/published application’s folder, AppContext.BaseDirectory is usually the clearer choice.