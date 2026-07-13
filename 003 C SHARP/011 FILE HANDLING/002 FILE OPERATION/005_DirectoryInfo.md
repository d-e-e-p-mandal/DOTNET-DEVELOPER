
## DirectoryInfo

`DirectoryInfo` is a class in the `System.IO` namespace used for working with a specific directory (folder) object.

Namespace:

```cs
using System.IO;
```

---

### What is DirectoryInfo?

`DirectoryInfo` provides detailed information about a folder and allows folder operations using an object-oriented approach.

Unlike `Directory`, `DirectoryInfo` requires object creation.

---

### Object Creation

```cs
DirectoryInfo dir =
    new DirectoryInfo("Data");
```

---

### Purpose

Used to:

- Get folder information
- Create folders
- Delete folders
- Move folders
- Rename folders
- Access files
- Access subfolders

---

### Class Type

```cs
public sealed class DirectoryInfo
```

Object Required:

```cs
DirectoryInfo dir =
    new DirectoryInfo("Data");
```

---

### Example

```cs
DirectoryInfo dir =
    new DirectoryInfo("Data");

Console.WriteLine(
    dir.Name);
```

Output:

```text
Data
```

---

## Common Properties

### Name

Gets folder name.

```cs
dir.Name
```

Output:

```text
Data
```

---

### FullName

Gets complete folder path.

```cs
dir.FullName
```

Output:

```text
C:\Projects\Data
```

---

### Parent

Gets parent directory.

```cs
dir.Parent
```

Output:

```text
C:\Projects
```

---

### Exists

Checks folder existence.

```cs
dir.Exists
```

Output:

```text
true
false
```

---

### CreationTime

Gets folder creation date.

```cs
dir.CreationTime
```

Output:

```text
01-01-2025
```

---

### LastWriteTime

Gets last modified date.

```cs
dir.LastWriteTime
```

Output:

```text
02-01-2025
```

---

### Root

Gets root drive.

```cs
dir.Root
```

Output:

```text
C:\
```

---

### Attributes

Gets folder attributes.

```cs
dir.Attributes
```

Output:

```text
Directory
ReadOnly
Hidden
```

---

## Common Methods

### Create()

Creates folder.

```cs
DirectoryInfo dir =
    new DirectoryInfo("Data");

dir.Create();
```

Output:

```text
Folder Created
```

---

### Delete()

Deletes folder.

```cs
dir.Delete();
```

Output:

```text
Folder Deleted
```

---

### Delete(true)

Deletes folder and contents.

```cs
dir.Delete(true);
```

Meaning:

```text
Delete Folder
+
Delete Files
+
Delete Subfolders
```

---

### MoveTo()

Moves folder.

```cs
dir.MoveTo("Backup");
```

Result:

```text
Data
 ↓
Backup
```

---

### Rename Folder

```cs
DirectoryInfo dir =
    new DirectoryInfo("Data");

dir.MoveTo("NewData");
```

Result:

```text
Data
 ↓
NewData
```

---

### CreateSubdirectory()

Creates subfolder.

```cs
dir.CreateSubdirectory(
    "Reports");
```

Result:

```text
Data
 └── Reports
```

---

### GetFiles()

Gets files inside folder.

```cs
FileInfo[] files =
    dir.GetFiles();
```

---

### Example

```cs
FileInfo[] files =
    dir.GetFiles();

foreach(FileInfo file in files)
{
    Console.WriteLine(
        file.Name);
}
```

Output:

```text
Employee.txt
Report.pdf
```

---

### GetDirectories()

Gets subfolders.

```cs
DirectoryInfo[] folders =
    dir.GetDirectories();
```

---

### Example

```cs
DirectoryInfo[] folders =
    dir.GetDirectories();

foreach(DirectoryInfo folder
        in folders)
{
    Console.WriteLine(
        folder.Name);
}
```

Output:

```text
Images
Reports
Logs
```

---

### Refresh()

Reloads latest folder information.

```cs
dir.Refresh();
```

Used after changes.

---

## Common Properties List

```cs
dir.Name

dir.FullName

dir.Parent

dir.Root

dir.Exists

dir.CreationTime

dir.LastWriteTime

dir.Attributes
```

---

## Common Methods List

```cs
dir.Create()

dir.Delete()

dir.Delete(true)

dir.MoveTo()

dir.CreateSubdirectory()

dir.GetFiles()

dir.GetDirectories()

dir.Refresh()
```

---

## Return Types

| Method | Return Type |
|----------|------------|
| Create() | void |
| Delete() | void |
| Delete(true) | void |
| MoveTo() | void |
| CreateSubdirectory() | DirectoryInfo |
| GetFiles() | FileInfo[] |
| GetDirectories() | DirectoryInfo[] |
| Refresh() | void |

---

## Example Folder Structure

```text
Data
│
├── Employee.txt
├── Report.pdf
│
├── Images
│
├── Logs
```

---

## Does DirectoryInfo Have Interface?

No direct interface.

Definition:

```cs
public sealed class DirectoryInfo
```

But it inherits:

```text
Object
   ↓
MarshalByRefObject
   ↓
FileSystemInfo
   ↓
DirectoryInfo
```

---

## Inheritance Hierarchy

```text
Object
   ↓
MarshalByRefObject
   ↓
FileSystemInfo
   ↓
DirectoryInfo
```

---

## Directory vs DirectoryInfo

| Directory | DirectoryInfo |
|------------|------------|
| Static Class | Object Class |
| No Object Required | Object Required |
| Simple Operations | Detailed Information |
| Static Methods | Instance Methods |
| Quick Usage | Object-Oriented Usage |

---

## When To Use DirectoryInfo?

Use DirectoryInfo when:

```text
Need Folder Information

Need Folder Properties

Need Multiple Operations
On Same Folder

Need Object-Oriented Code
```

Examples:

```text
Get Folder Name

Get Creation Time

Get Subfolders

Get Files

Move Folder

Rename Folder
```

---

## Quick Revision

```text
DirectoryInfo
      ↓
Folder Object

Purpose
      ↓
Create Folder
Delete Folder
Move Folder
Rename Folder
Get Files
Get Subfolders

Object Required?
      ↓
Yes

Common Properties
      ↓
Name
FullName
Parent
CreationTime

Common Methods
      ↓
Create()
Delete()
MoveTo()
GetFiles()
GetDirectories()
```