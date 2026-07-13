# Stream:

**Stream**
    ↓
Base Data Flow

**Byte Stream**
    ↓
Images
Videos
PDF

**Character Stream**
    ↓
Text
JSON
XML

**FileStream**
    ↓
Read()
Write()
Seek()
Flush()
Close()

**StreamReader**
    ↓
Read()
ReadLine()
ReadToEnd()

**StreamWriter**
    ↓
Write()
WriteLine()
Flush()


# 8. Stream Basics

## What is Stream?
- A Stream is a flow of data from one place to another.
- Simple Meaning: Data Pipeline


**Flow:**
```text
Source
   ↓
Stream
   ↓
Destination
```

**Examples:**

```text
File → Stream → Application
Application → Stream → File
Network → Stream → Application
Memory → Stream → Application
```

---

## Why Stream Used?

- Used when reading or writing data.

**Examples:**
- Files
- Network Data
- Memory Data
- Images
- Videos
- PDF Files

---

## Stream Hierarchy

```text
Object
   ↓
MarshalByRefObject
   ↓
Stream
   ↓
├── FileStream
├── MemoryStream
├── NetworkStream
├── BufferedStream
```

---

## Byte Stream

Works with raw bytes.

Data Type:

```cs
byte[]
```

**Example:**
- Images
- PDF Files
- Videos
- Audio Files

Example:

```cs
byte[] data =
{
    65,
    66,
    67
};
```

Output:
```text
ABC
```

---

## Character Stream
- Works with text characters.
Data Type: char or string

**Example:**
- Text Files
- CSV Files
- JSON Files
- XML Files

**Example:**

```text
Hello World
```

---

# Stream Common Properties

## CanRead

```cs
stream.CanRead
```

Purpose:

```text
Can Read Data?
```

Returns:

```cs
bool
```

---

## CanWrite

```cs
stream.CanWrite
```

Purpose:

```text
Can Write Data?
```

Returns:

```cs
bool
```

---

## CanSeek

```cs
stream.CanSeek
```

Purpose:

```text
Can Move Position?
```

Returns:

```cs
bool
```

---

## Length

```cs
stream.Length
```

Purpose:

```text
Total Size
```

Returns:

```cs
long
```

---

## Position

```cs
stream.Position
```

Purpose:

```text
Current Cursor Position
```

Returns:

```cs
long
```

---

# 9. FileStream

## What is FileStream?

Used to read and write files at byte level.

Namespace:

```cs
using System.IO;
```

---

## Create FileStream

### Create New File

```cs
FileStream fs =
    new FileStream(
        "test.txt",
        FileMode.Create);
```

---

### Open Existing File

```cs
FileStream fs =
    new FileStream(
        "test.txt",
        FileMode.Open);
```

---

### Recommended

```cs
using FileStream fs =
    new FileStream(
        "test.txt",
        FileMode.Open);
```

---

## FileMode Options

```cs
FileMode.Create

FileMode.Open

FileMode.Append

FileMode.CreateNew

FileMode.Truncate

FileMode.OpenOrCreate
```

---

## Read()

### Purpose

Read bytes from file.

### Syntax

```cs
fs.Read(
    buffer,
    offset,
    count);
```

---

### Example

```cs
byte[] buffer =
    new byte[100];

int bytesRead =
    fs.Read(
        buffer,
        0,
        buffer.Length);
```

---

### Return Type

```cs
int
```

Meaning:

```text
Number Of Bytes Read
```

---

## Write()

### Purpose

Write bytes into file.

### Syntax

```cs
fs.Write(
    buffer,
    offset,
    count);
```

---

### Example

```cs
byte[] data =
    Encoding.UTF8.GetBytes(
        "Hello");

fs.Write(
    data,
    0,
    data.Length);
```

---

### Return Type

```cs
void
```

---

## Seek()

### Purpose

Move current position.

### Syntax

```cs
fs.Seek(
    offset,
    SeekOrigin.Begin);
```

---

### Example

```cs
fs.Seek(
    10,
    SeekOrigin.Begin);
```

Meaning:

```text
Move Cursor To Byte 10
```

---

## SeekOrigin Options

```cs
SeekOrigin.Begin

SeekOrigin.Current

SeekOrigin.End
```

---

## Flush()

### Purpose

Force write buffered data.

### Example

```cs
fs.Flush();
```

Meaning:

```text
Save Pending Data Immediately
```

---

## Close()

### Purpose

Close stream.

### Example

```cs
fs.Close();
```

Meaning:

```text
Release File Resources
```

---

## Common FileStream Methods

```cs
Read()

Write()

Seek()

Flush()

Close()

ReadAsync()

WriteAsync()

CopyTo()
```

---

# 10. StreamReader

## What is StreamReader?

Used for reading text files.

Works on:

```text
Characters

Strings

Text Files
```

---

## Create StreamReader

```cs
StreamReader reader =
    new StreamReader(
        "test.txt");
```

---

### Recommended

```cs
using StreamReader reader =
    new StreamReader(
        "test.txt");
```

---

===============================

## Read()

### Purpose

Read one character.

### Example

```cs
int ch =
    reader.Read();
```

Output:

```text
ASCII Value
```

---

## ReadLine()

### Purpose

Read one line.

### Example

```cs
string line =
    reader.ReadLine();
```

File:

```text
Hello
World
```

Output:

```text
Hello
```

---

## ReadToEnd()

### Purpose

Read complete file.

### Example

```cs
string text =
    reader.ReadToEnd();
```

Output:

```text
Entire File Content
```

---

## Other Useful Methods

### Peek()

```cs
reader.Peek();
```

Purpose:

```text
See Next Character
Without Reading
```

---

### Close()

```cs
reader.Close();
```

---

## Common StreamReader Methods

```cs
Read()

ReadLine()

ReadToEnd()

Peek()

Close()
```

---

====================================================

# 11. StreamWriter

## What is StreamWriter?

Used to write text data into files.

Works on:

```text
Characters

Strings

Text Files
```

---

## Create StreamWriter

```cs
StreamWriter writer =
    new StreamWriter(
        "test.txt");
```

---

### Recommended

```cs
using StreamWriter writer =
    new StreamWriter(
        "test.txt");
```

---

## Write()

### Purpose

Write text.

### Example

```cs
writer.Write(
    "Hello");
```

Output:

```text
Hello
```

---

## WriteLine()

### Purpose

Write text with new line.

### Example

```cs
writer.WriteLine(
    "Hello");

writer.WriteLine(
    "World");
```

File:

```text
Hello
World
```

---

## Flush()

### Purpose

Force save buffered data.

### Example

```cs
writer.Flush();
```

Meaning:

```text
Write Pending Data Immediately
```

---

## Close()

### Purpose

Close writer.

### Example

```cs
writer.Close();
```

---

## Other Useful Methods

### WriteAsync()

```cs
await writer.WriteAsync(
    "Hello");
```

---

### WriteLineAsync()

```cs
await writer.WriteLineAsync("Hello");
```

---

## Common StreamWriter Methods

```cs
Write()

WriteLine()

Flush()

Close()

WriteAsync()

WriteLineAsync()
```

---

# Stream vs StreamReader vs StreamWriter

| Type | Purpose |
|--------|---------|
| Stream | Base Data Stream |
| FileStream | Byte Level File Access |
| StreamReader | Read Text Files |
| StreamWriter | Write Text Files |

---