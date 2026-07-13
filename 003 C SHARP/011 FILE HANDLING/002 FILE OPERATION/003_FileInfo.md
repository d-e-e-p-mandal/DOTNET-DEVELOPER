
## What is FileInfo?

`FileInfo` provides detailed information about a file and allows file operations using an object-oriented approach.

Unlike `File`, `FileInfo` requires object creation.

---

### Object Creation

```cs
FileInfo file = new FileInfo("test.txt");
```

---

### Purpose

Used to:
- Get file information
- Create file
- Delete file
- Copy file
- Move file
- Rename file
- Access file properties

---

### Class Type

```cs
public sealed class FileInfo
```

Object Required:

```cs
FileInfo file = new FileInfo("test.txt");
```

---

### Example

```cs
FileInfo file = new FileInfo("test.txt");

Console.WriteLine(file.Name);
```
**Output:**
```text
test.txt
```

---

## Common Properties

### Name
- Gets file name.

```cs
file.Name
```
**Output:**
```text
test.txt
```

---

### FullName
- Gets complete path.

```cs
file.FullName
```

**Output:**
```text
C:\Data\test.txt
```

---

### Extension
- Gets file extension.

```cs
file.Extension
```

**Output:**

```text
.txt
```

---

### Length
- Gets file size in bytes.

```cs
file.Length
```

**Output:**
```text
1024
```

---

### DirectoryName
- Gets directory path.

```cs
file.DirectoryName
```

**Output:**
```text
C:\Data
```

---

### Exists
- Checks whether file exists.

```cs
file.Exists
```

**Output:**

```text
true
false
```

---

### CreationTime
- Gets file creation date.

```cs
file.CreationTime
```

**Output:**

```text
01-01-2025
```

---

### LastWriteTime

- Gets last modified date.

```cs
file.LastWriteTime
```

**Output:**

```text
02-01-2025
```

---

### IsReadOnly
- Checks or sets read-only mode.

```cs
file.IsReadOnly
```

**Output:**

```text
true
false
```

---

## Common Methods

### Create()
- Creates a new file.

```cs
FileInfo file = new FileInfo("test.txt");
file.Create();
```

**Output:**
```text
test.txt Created
Return Type:
```

**Return Type:** FileStream

---

### Delete()
- Deletes file.

```cs
file.Delete();
```

**Return Type:** void

---

### CopyTo()
- Copies file.

```cs
file.CopyTo("backup.txt");
```

**Return Type:** FileInfo


---

### MoveTo()
- Moves file.

```cs
file.MoveTo("Data\\test.txt");
```
**Return Type:** void


---

### Rename File

- No Rename() method exists.

Use:
```cs
file.MoveTo("newtest.txt");
```

**Result:**
```text
File Renamed
```

---

### Refresh()
- Reload file information.

```cs
file.Refresh();
```

- Used after file changes.

---

## Create Example

```cs
FileInfo file = new FileInfo("test.txt");

file.Create();
```

---

## Delete Example

```cs
FileInfo file =
    new FileInfo("test.txt");

file.Delete();
```

---

## Copy Example

```cs
FileInfo file = new FileInfo("test.txt");

file.CopyTo("backup.txt");
```

---

## Move Example

```cs
FileInfo file = new FileInfo("test.txt");
file.MoveTo("Data\\test.txt");
```

---

## Property Example

```cs
FileInfo file = new FileInfo("test.txt");

Console.WriteLine(file.Name);

Console.WriteLine(file.Length);

Console.WriteLine(file.Extension);
```

**Output:**

```text
test.txt
2048
.txt
```

---

## Common Properties List

```cs
file.Name
file.FullName
file.Extension
file.Length
file.DirectoryName
file.Exists
file.CreationTime
file.LastWriteTime
file.IsReadOnly
```

---

## Common Methods List

```cs
file.Create()
file.Delete()
file.CopyTo()
file.MoveTo()
file.Refresh()
```

---

## File vs FileInfo

| File | FileInfo |
|--------|--------|
| Static Class | Object Class |
| No Object Required | Object Required |
| Simple Operations | Detailed Operations |
| Faster For Small Tasks | Better For Repeated Tasks |
| Static Methods | Instance Methods |

---

## When To Use FileInfo?

Use FileInfo when:
- Need File Information
- Need Multiple Operations On Same File
- Need Object-Oriented Code
- Need File Properties

**Examples:**
```text
Get File Size
Get Creation Date
Get Extension
Copy File
Move File
Rename File
```

---

## Quick Revision

```text
FileInfo
     ↓
File Object

Purpose
     ↓
Create
Delete
Copy
Move
Rename
Get File Information

Object Required?
     ↓
Yes

Common Properties
     ↓
Name
Length
Extension
CreationTime

Common Methods
     ↓
Create()
Delete()
CopyTo()
MoveTo()
Refresh()
```