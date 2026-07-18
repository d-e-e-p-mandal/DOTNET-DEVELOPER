
# C# Path Class (System.IO):

- The `Path` class is a static class provided by the .NET Framework inside the `System.IO` namespace.
- It is used to work with file and folder path strings. The Path class helps developers create, manipulate, analyze, and retrieve information from file paths safely and efficiently.
- The Path class does not create files or directories. It only works with path strings.

**Namespace:**
```csharp
using System.IO;
```


**Why Path Class is Needed:**
- When working with files and folders, paths are frequently required.

**Without Path Class:**
```csharp
string path = "Data" + "\\" + "Employee.txt";
```

**Problems:**
- Hard to read
- Difficult to maintain
- Platform dependent
- Easy to make mistakes

**Using Path Class:**
```csharp
string path = Path.Combine("Data", "Employee.txt");
```

**Output:**
```text
Data\Employee.txt
```

**Benefits:**

- Safer path creation
- Better readability
- Platform independent
- Reduces coding errors

---

# Path Class Architecture

```text
System
 └── IO
      └── Path
```

- The Path class is `static`.

**Therefore:**
```csharp
Path.Combine(...)
Path.GetFileName(...)
```

- No object creation is required.

**Incorrect:**
```csharp
Path p = new Path();
```

**Correct:**
```csharp
Path.Combine(...)
```

---

# Commonly Used Methods

## 1. Path.Combine()

**Purpose:**
- Combines multiple path segments into one complete path.

**Syntax:**
```csharp
Path.Combine(path1, path2);
```

**Example:**
```csharp
string path = Path.Combine("Data", "Employee.txt");
Console.WriteLine(path);
```

**Output:** `Data\Employee.txt`


### Multiple Segments
```csharp
string path = Path.Combine(
    "C:",
    "Users",
    "Deep",
    "Documents",
    "File.txt"
);

Console.WriteLine(path);
```

**Output:** `C:\Users\Deep\Documents\File.txt`


### Real World Usage

```csharp
string filePath = Path.Combine(
    Environment.CurrentDirectory,
    "Data",
    "Employee.txt"
);
```

---

## 2. Path.GetFileName()

**Purpose:**
- Returns only the file name from a full path.

**Example:**
```csharp
string fileName =
Path.GetFileName("Data\\Employee.txt");
Console.WriteLine(fileName);
```

**Output:** `Employee.txt`

**Real Example:**
```csharp
string path = "C:\\Project\\Reports\\Report.pdf";
Console.WriteLine(Path.GetFileName(path));
```

**Output:** `Report.pdf`


---

## 3. Path.GetExtension()

**Purpose:**
- Returns the file extension.

**Example:**
```csharp
string extension =
Path.GetExtension("Data\\Test.txt");
Console.WriteLine(extension);
```

**Output:** `.txt`


### More Examples
```csharp
Path.GetExtension("Photo.jpg");
```
**Output:** `.jpg`


```csharp
Path.GetExtension("Video.mp4");
```
**Output:** `.mp4`


```csharp
Path.GetExtension("Document.pdf");
```

**Output:** `.pdf`


---

## 4. Path.GetDirectoryName()

**Purpose:**
- Returns only the directory path.

**Example:**

```csharp
string directory =
Path.GetDirectoryName("C:\\Data\\Employee.txt");
Console.WriteLine(directory);
```
**Output:** `C:\Data`


### Diagram

```text
C:\Data\Employee.txt
    │      │
    │      └── File Name
    │
    └── Directory Name
```

---

## 5. Path.GetFileNameWithoutExtension()

**Purpose:**
- Returns file name without extension.

**Example:**
```csharp
string fileName =
Path.GetFileNameWithoutExtension("Employee.txt");
Console.WriteLine(fileName);
```

**Output:**
```text
Employee
```

### Diagram
```text
Employee.txt
    │     │
    │     └── Extension
    │
    └── File Name
```

---

## 6. Path.GetTempPath()

### Purpose

- Returns the operating system temporary folder path.

### Example

```csharp
string tempPath = Path.GetTempPath();

Console.WriteLine(tempPath);
```

Possible Output:

```text
C:\Users\Admin\AppData\Local\Temp\
```

### Uses

- Temporary files
- Cache storage
- Logs
- Upload processing

Example:

```csharp
string logFile =
Path.Combine(Path.GetTempPath(), "log.txt");
```

---

## 7. Path.GetRandomFileName()

### Purpose

Generates a random file name.

### Example

```csharp
string randomName = Path.GetRandomFileName();

Console.WriteLine(randomName);
```

Possible Output:

```text
f4jk3n5a.tmp
```

### Use Cases

- Temporary files
- Unique file creation
- Upload processing
- Session storage

---

## 8. Path.ChangeExtension()

### Purpose

Changes file extension.

### Example

```csharp
string file = Path.ChangeExtension("Report.txt", "pdf");

Console.WriteLine(file);
```

**Output:**
```text
Report.pdf
```

---

## 9. Path.HasExtension()

### Purpose

Checks whether a file has an extension.

### Example

```csharp
bool result =
Path.HasExtension("Employee.txt");

Console.WriteLine(result);
```

Output:

```text
True
```

---

## 10. Path.GetFullPath()

### Purpose

Returns absolute path.

### Example

```csharp
string fullPath = Path.GetFullPath("Employee.txt");

Console.WriteLine(fullPath);
```

Possible Output:

```text
C:\Project\Employee.txt
```

---

# Important Path Properties

## Path.DirectorySeparatorChar

Returns the directory separator used by the operating system.

```csharp
Console.WriteLine(Path.DirectorySeparatorChar);
```

Output (Windows):

```text
\
```

---

## Path.AltDirectorySeparatorChar
- Returns alternative directory separator.

```csharp
Console.WriteLine(Path.AltDirectorySeparatorChar);
```

Output:

```text
/
```

---

## Path.PathSeparator

Returns separator used between multiple paths.

```csharp
Console.WriteLine(Path.PathSeparator);
```

Output:

```text
;
```

Example:

```text
C:\Folder1;C:\Folder2
```

---

## Path.VolumeSeparatorChar

Returns drive separator.

```csharp
Console.WriteLine(Path.VolumeSeparatorChar);
```

Output:

```text
:
```

Example:

```text
C:
D:
E:
```

---

# Real Project Examples

## Example 1: Creating File Path

```csharp
string path = Path.Combine("Data","Employee.txt");
```

Output:

```text
Data\Employee.txt
```

---

## Example 2: Reading File

```csharp
string path =
Path.Combine("Data","Employee.txt");

if(File.Exists(path))
{
    string content = File.ReadAllText(path);

    Console.WriteLine(content);
}
```

---

## Example 3: Creating Temporary File

```csharp
string tempFile =
Path.Combine(Path.GetTempPath(), Path.GetRandomFileName());

Console.WriteLine(tempFile);
```

---

# Path vs File vs Directory

| Class | Purpose |
|---------|---------|
| Path | Path String Operations |
| File | File Operations |
| Directory | Folder Operations |

Example:

```csharp
string path =
Path.Combine(
    "Data",
    "Test.txt"
);

File.WriteAllText(
    path,
    "Hello World"
);
```

Explanation:

```text
Path -> Creates path string

File -> Writes data into file
```

---

# Common Interview Questions

## What is Path Class?

A static class in System.IO used to manipulate file and folder path strings.

---

## Is Path Class Static?

Yes.

```csharp
Path.Combine(...)
```

No object creation is required.

---

## Does Path Class Create Files?

No.

It only creates and manipulates path strings.

---

## Difference Between Path and File Class?

Path:

```csharp
Path.Combine(...)
```

Works with path strings.

File:

```csharp
File.WriteAllText(...)
```

Performs file operations.

---

## Why Use Path.Combine Instead of String Concatenation?

Because it:

- Automatically adds separators
- Avoids path formatting mistakes
- Improves readability
- Works across operating systems

---

# Best Practices

1. Always use Path.Combine().
2. Avoid hardcoded paths.
3. Use GetFullPath() for absolute paths.
4. Use GetRandomFileName() for temporary files.
5. Use GetExtension() before validating file types.
6. Use GetFileNameWithoutExtension() when renaming files.
7. Never manually concatenate path separators.

---

# Summary

```text
Path Class

Purpose:
✓ Build Paths
✓ Extract File Names
✓ Extract Extensions
✓ Get Folder Names
✓ Create Temporary Paths
✓ Generate Random File Names

Important Methods:

✓ Path.Combine()
✓ Path.GetFileName()
✓ Path.GetExtension()
✓ Path.GetDirectoryName()
✓ Path.GetFileNameWithoutExtension()
✓ Path.GetTempPath()
✓ Path.GetRandomFileName()
✓ Path.ChangeExtension()
✓ Path.HasExtension()
✓ Path.GetFullPath()

Related Classes:

✓ File
✓ Directory
```

# Memory Trick

```text
Path      → Path Information

File      → File Operations

Directory → Folder Operations
```

Remember:

The Path class never creates, deletes, reads, or writes files. It only helps manage and analyze path strings safely.