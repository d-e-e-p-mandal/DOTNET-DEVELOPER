## File:

### What is File Class?
The File class provides ready-made methods to:
- Create files
- Read files
- Write files
- Copy files
- Move files
- Delete files

without creating any object.

---

### File Class Type

```cs
public static class File
```
- Since it is a static class: No Object Creation Required


**Correct:**

```cs
File.Create("test.txt");
```
**Wrong:**

```cs
File file = new File();
```

---

## File.Create()
- Creates a new file.

### Syntax

```cs
File.Create("test.txt");
```

**Return Type:** FileStream


### Example

```cs
File.Create("test.txt");
```

**Output:**

```text
test.txt Created
```

---

## File.Exists()
- Checks whether a file exists.

### Syntax

```cs
File.Exists("test.txt");
```

**Return Type:** bool

### Example

```cs
bool exists = File.Exists("test.txt");
```

**Output:**

```text
true
false
```

---

## File.ReadAllText()
- Reads complete file content.

### Syntax

```cs
File.ReadAllText("test.txt");
```

**Return Type:** string


### Example

```cs
string data = File.ReadAllText("test.txt");
```

Output:

```text
Hello World
```

---

## File.ReadAllLines()
- Reads all lines from a file.

### Syntax

```cs
File.ReadAllLines("test.txt");
```

**Return Type:** string[]


### Example

```cs
string[] lines = File.ReadAllLines("test.txt");
```

File:

```text
Line 1
Line 2
Line 3
```

Output:

```text
["Line 1","Line 2","Line 3"]
```

---

## File.WriteAllText()
- Writes text into a file.
- If file exists: Old Content Replaced

### Syntax

```cs
File.WriteAllText(
    "test.txt",
    "Hello");
```

**Return Type:** void

### Example

```cs
File.WriteAllText("test.txt", "Hello World");
```

File:

```text
Hello World
```

---

## File.WriteAllLines()
- Writes multiple lines into a file.

### Syntax

```cs
File.WriteAllLines("test.txt", lines);
```

**Return Type:** void

### Example

```cs
File.WriteAllLines("test.txt", new string[]
    {
        "Line 1",
        "Line 2",
        "Line 3"
    });
```

File:

```text
Line 1
Line 2
Line 3
```

---

## File.AppendAllText()

### Purpose

- Adds new text at the end of a file.
- Existing content remains unchanged.

### Syntax

```cs
File.AppendAllText("test.txt", "New Data");
```

**Return Type:** void

### Example

Before:

```text
Hello
```

Code:

```cs
File.AppendAllText("test.txt", "\nWorld");
```

After:

```text
Hello
World
```

---

## File.Copy()
- Copies file from one location to another.

### Syntax

```cs
File.Copy(source, destination);
```

**Return Type:** void

### Example

```cs
File.Copy("test.txt", "backup.txt");
```

Result:

```text
test.txt
backup.txt
```

---

## File.Move()
- Moves file to another location.
- Can also rename a file.

### Syntax

```cs
File.Move(source, destination); // relative path
File.Move("Data\\file.txt", "..\\file.txt"); // move to parent folder
```

**Return Type:** void


### Example
```cs
File.Move("test.txt", "Data\\test.txt");
```

Result:

```text
File Moved
```

---

### Rename Example

```cs
File.Move("test.txt", "newtest.txt");
```

Result:

```text
File Renamed
```

---

## File.Delete()
- Deletes a file.

### Syntax

```cs
File.Delete("test.txt");
```

**Return Type :**void

### Example

```cs
File.Delete("test.txt");
```

Result:

```text
File Deleted
```
---

### Does File Class Have Interface?

No.

```text
File Class
    ↓
Static Class
    ↓
Cannot Implement Interface
```