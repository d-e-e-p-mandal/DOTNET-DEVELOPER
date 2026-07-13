
## Directory:

### What is Directory?
- `Directory` is a static class in the `System.IO` namespace used for folder (directory) operations.

The `Directory` class provides methods to:

- Create folders
- Delete folders
- Move folders
- Check folder existence
- Get files from folders
- Get subfolders

without creating an object.

---

### Class Type

```cs
public static class Directory
```

- Since it is a static class: No Object Creation Required

Correct:
```cs
Directory.CreateDirectory("Data");
```
Wrong:s
```cs
Directory dir =
    new Directory();
```

---

### Purpose

Used to:s
- Manage folders
- Organize files
- Access directory contents
- Create project structure

---

## Common Methods

### CreateDirectory()
- Creates a new folder.

```cs
Directory.CreateDirectory("Data");
```

Output:

```text
Data Folder Created
```

---

### Create Nested Folders

```cs
Directory.CreateDirectory("Data\\Employee\\Files");
```

Result:

```text
Data
 └── Employee
       └── Files
```

---

### Delete()
- Deletes a folder.

```cs
Directory.Delete("Data");
```

Output:

```text
Folder Deleted
```

---

### Delete Non-Empty Folder

```cs
Directory.Delete("Data", true);
```

Parameter:

```text
true
↓
Delete Folder And Contents
```

---

### Exists()
- Checks if folder exists.

```cs
bool exists = Directory.Exists("Data");
```

**Output:**

```text
true
false
```

---

### GetFiles()
- Returns files inside a folder.

```cs
string[] files = Directory.GetFiles("Data");
```

Output:
```text
Employee.txt
Report.pdf
Data.json
```

---

### Example

```cs
string[] files = Directory.GetFiles("Data");

foreach(var file in files)
{
    Console.WriteLine(file);
}
```

---

### GetDirectories()
- Returns subfolders.

```cs
string[] folders = Directory.GetDirectories("Data");
```
Output:

```text
Images
Reports
Logs
```

---

### Example

```cs
string[] folders = Directory.GetDirectories("Data");

foreach(var folder in folders)
{
    Console.WriteLine(folder);
}
```

---

### Move()

Moves or renames folder.

```cs
Directory.Move("Data", "Backup");
```

Result:

```text
Data
  ↓
Backup
```

---

### GetCurrentDirectory()
- Gets current working directory.

```cs
string path = Directory.GetCurrentDirectory();
```

Output:

```text
C:\Projects\TestApp
```

---

### SetCurrentDirectory()

- Changes current working directory.

```cs
Directory.SetCurrentDirectory("D:\\Data");
```

---

### GetParent()

Gets parent folder.

```cs
DirectoryInfo parent = Directory.GetParent("C:\\Data\\Files");
```

Output:

```text
C:\Data
```

---

### GetCreationTime()
- Gets folder creation time.

```cs
DateTime date =Directory.GetCreationTime("Data");
```

---

### GetLastWriteTime()

Gets last modified time.

```cs
DateTime date = Directory.GetLastWriteTime("Data");
```

---

## Common Methods List

```cs
Directory.CreateDirectory()

Directory.Delete()

Directory.Exists()

Directory.GetFiles()

Directory.GetDirectories()

Directory.Move()

Directory.GetCurrentDirectory()

Directory.SetCurrentDirectory()

Directory.GetParent()

Directory.GetCreationTime()

Directory.GetLastWriteTime()
```

---

## Return Types

| Method | Return Type |
|----------|------------|
| CreateDirectory() | DirectoryInfo |
| Delete() | void |
| Exists() | bool |
| GetFiles() | string[] |
| GetDirectories() | string[] |
| Move() | void |
| GetCurrentDirectory() | string |
| SetCurrentDirectory() | void |
| GetParent() | DirectoryInfo |
| GetCreationTime() | DateTime |
| GetLastWriteTime() | DateTime |

---

## Example Project Structure

```text
Project
│
├── Data
│      ├── Employee.txt
│      ├── Report.pdf
│
├── Images
│      ├── Photo.jpg
│
├── Logs
│      ├── Error.txt
```

---

## Does Directory Have Interface?

No.

```text
Directory
    ↓
Static Class
    ↓
No Interface
```

Definition:

```cs
public static class Directory
```

---

## Directory vs DirectoryInfo

| Directory | DirectoryInfo |
|------------|------------|
| Static Class | Object Class |
| No Object Required | Object Required |
| Simple Operations | Detailed Operations |
| Quick Access | More Information |
| Static Methods | Instance Methods |

---

## When To Use Directory?

Use Directory when:
- Create Folder
- Delete Folder
- Check Folder Exists
- Get Files
- Get Subfolders
- Move Folder
```

---
