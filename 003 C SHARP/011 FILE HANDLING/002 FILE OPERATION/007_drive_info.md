# C# DriveInfo Class:

# Introduction

The `DriveInfo` class is available in the `System.IO` namespace and is used to retrieve information about storage drives present in a computer system.

A drive can be:

- Hard Disk Drive (HDD)
- Solid State Drive (SSD)
- USB Drive
- CD/DVD Drive
- Network Drive
- Removable Storage

The DriveInfo class helps applications monitor disk space, check drive status, and display storage information.

Namespace:

```csharp
using System.IO;
```

---

# Why DriveInfo is Needed

Many applications need information about storage devices.

Examples:

- Checking available disk space before file upload
- Monitoring server storage
- Displaying drive information
- Backup software
- Disk management tools

Without DriveInfo:

```csharp
// Difficult to retrieve drive information manually
```

With DriveInfo:

```csharp
DriveInfo drive = new DriveInfo("C");
```

---

# DriveInfo Class Architecture

```text
System
 └── IO
      └── DriveInfo
```

---

# Creating DriveInfo Object

## Syntax

```csharp
DriveInfo drive = new DriveInfo("C");
```

or

```csharp
DriveInfo drive = new DriveInfo("D");
```

---

# Example

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        DriveInfo drive = new DriveInfo("C");

        Console.WriteLine(drive.Name);
    }
}
```

Output:

```text
C:\
```

---

# Important Properties

## 1. Name

### Purpose

Returns the drive name.

### Example

```csharp
DriveInfo drive = new DriveInfo("C");

Console.WriteLine(drive.Name);
```

Output:

```text
C:\
```

---

## 2. DriveType

### Purpose

Returns the type of drive.

### Example

```csharp
DriveInfo drive = new DriveInfo("C");

Console.WriteLine(drive.DriveType);
```

Output:

```text
Fixed
```

---

### Possible Drive Types

| Drive Type | Description |
|------------|-------------|
| Fixed | HDD or SSD |
| Removable | USB Drive |
| CDRom | CD/DVD Drive |
| Network | Network Drive |
| Ram | RAM Disk |
| Unknown | Unknown Drive |

---

## 3. TotalSize

### Purpose

Returns total drive size in bytes.

### Example

```csharp
DriveInfo drive = new DriveInfo("C");

Console.WriteLine(drive.TotalSize);
```

Output:

```text
512110190592
```

(Example Value)

---

### Convert to GB

```csharp
DriveInfo drive = new DriveInfo("C");

double sizeGB =
drive.TotalSize / (1024.0 * 1024 * 1024);

Console.WriteLine(sizeGB);
```

Output:

```text
476.94 GB
```

---

## 4. AvailableFreeSpace

### Purpose

Returns free space available to the current user.

### Example

```csharp
DriveInfo drive = new DriveInfo("C");

Console.WriteLine(
drive.AvailableFreeSpace
);
```

Output:

```text
180000000000
```

---

### Convert Free Space to GB

```csharp
double freeGB =
drive.AvailableFreeSpace /
(1024.0 * 1024 * 1024);

Console.WriteLine(freeGB);
```

Output:

```text
167.65 GB
```

---

## 5. TotalFreeSpace

### Purpose

Returns total free space on the drive.

### Example

```csharp
Console.WriteLine(
drive.TotalFreeSpace
);
```

Output:

```text
180000000000
```

---

# Difference Between AvailableFreeSpace and TotalFreeSpace

| Property | Meaning |
|-----------|----------|
| AvailableFreeSpace | Space available to current user |
| TotalFreeSpace | Total free space on drive |

Usually both are the same for personal computers.

---

## 6. VolumeLabel

### Purpose

Returns the drive label name.

### Example

```csharp
DriveInfo drive = new DriveInfo("C");

Console.WriteLine(
drive.VolumeLabel
);
```

Output:

```text
Windows
```

Example:

```text
Windows
Data
Backup
LocalDisk
```

---

## 7. IsReady

### Purpose

Checks whether the drive is accessible.

### Example

```csharp
DriveInfo drive = new DriveInfo("D");

Console.WriteLine(
drive.IsReady
);
```

Output:

```text
True
```

or

```text
False
```

---

### Why IsReady is Important

Example:

```csharp
DriveInfo drive = new DriveInfo("E");

if(drive.IsReady)
{
    Console.WriteLine(drive.TotalSize);
}
```

This prevents exceptions when no USB or DVD is inserted.

---

## 8. DriveFormat

### Purpose

Returns file system type.

### Example

```csharp
Console.WriteLine(
drive.DriveFormat
);
```

Output:

```text
NTFS
```

Possible Values:

```text
NTFS
FAT32
exFAT
ReFS
```

---

## 9. RootDirectory

### Purpose

Returns root folder of drive.

### Example

```csharp
Console.WriteLine(
drive.RootDirectory
);
```

Output:

```text
C:\
```

---

# Listing All Drives

One of the most common uses of DriveInfo.

## Example

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        DriveInfo[] drives =
        DriveInfo.GetDrives();

        foreach(DriveInfo drive in drives)
        {
            Console.WriteLine(
                drive.Name
            );
        }
    }
}
```

Output:

```text
C:\
D:\
E:\
```

---

# Display Complete Drive Information

```csharp
using System;
using System.IO;

class Program
{
    static void Main()
    {
        foreach(DriveInfo drive in DriveInfo.GetDrives())
        {
            if(drive.IsReady)
            {
                Console.WriteLine(
                    "Drive Name: " +
                    drive.Name
                );

                Console.WriteLine(
                    "Type: " +
                    drive.DriveType
                );

                Console.WriteLine(
                    "Format: " +
                    drive.DriveFormat
                );

                Console.WriteLine(
                    "Label: " +
                    drive.VolumeLabel
                );

                Console.WriteLine(
                    "Total Size: " +
                    drive.TotalSize
                );

                Console.WriteLine(
                    "Free Space: " +
                    drive.AvailableFreeSpace
                );

                Console.WriteLine();
            }
        }
    }
}
```

Sample Output:

```text
Drive Name: C:\
Type: Fixed
Format: NTFS
Label: Windows
Total Size: 512110190592
Free Space: 180000000000
```

---

# Real Project Use Cases

## 1. Check Storage Before Upload

```csharp
DriveInfo drive = new DriveInfo("C");

if(drive.AvailableFreeSpace > 1000000000)
{
    Console.WriteLine(
        "Enough Space Available"
    );
}
```

---

## 2. Server Monitoring

```csharp
DriveInfo drive = new DriveInfo("C");

double freeGB =
drive.AvailableFreeSpace /
(1024.0 * 1024 * 1024);

if(freeGB < 10)
{
    Console.WriteLine(
        "Disk Space Running Low"
    );
}
```

---

## 3. Backup Application

```csharp
DriveInfo usbDrive =
new DriveInfo("E");

if(usbDrive.IsReady)
{
    Console.WriteLine(
        "USB Connected"
    );
}
```

---

# Common Exceptions

## DriveNotFoundException

Occurs when drive does not exist.

Example:

```csharp
DriveInfo drive =
new DriveInfo("Z");
```

If Z drive doesn't exist:

```text
DriveNotFoundException
```

---

## IOException

Occurs when drive is not ready.

Example:

```csharp
DVD drive without disk inserted
```

---

# DriveInfo vs DirectoryInfo vs FileInfo

| Class | Purpose |
|---------|---------|
| DriveInfo | Drive Information |
| DirectoryInfo | Folder Information |
| FileInfo | File Information |

---

## Example

```csharp
DriveInfo drive =
new DriveInfo("C");
```

Works with:

```text
Drive Level
```

---

```csharp
DirectoryInfo dir =
new DirectoryInfo("Data");
```

Works with:

```text
Folder Level
```

---

```csharp
FileInfo file =
new FileInfo("Test.txt");
```

Works with:

```text
File Level
```

---

# Interview Questions

## What is DriveInfo?

A class in System.IO used to retrieve information about disk drives.

---

## Which namespace contains DriveInfo?

```csharp
System.IO
```

---

## How to get all available drives?

```csharp
DriveInfo.GetDrives();
```

---

## Which property returns free space?

```csharp
AvailableFreeSpace
```

---

## Which property returns drive type?

```csharp
DriveType
```

---

## Why use IsReady?

To verify that a drive is accessible before reading its properties.

---

## Which property returns file system type?

```csharp
DriveFormat
```

Example:

```text
NTFS
FAT32
exFAT
```

---

# Best Practices

1. Always check `IsReady` before accessing drive properties.
2. Convert bytes to GB for readable output.
3. Use `GetDrives()` to enumerate all drives.
4. Handle exceptions for unavailable drives.
5. Monitor free space in production servers.

---

# Summary

```text
DriveInfo Class

Namespace:
System.IO

Purpose:
✓ Get Drive Information
✓ Check Drive Status
✓ Monitor Disk Space
✓ Display Storage Details

Important Properties:

✓ Name
✓ DriveType
✓ TotalSize
✓ AvailableFreeSpace
✓ TotalFreeSpace
✓ VolumeLabel
✓ IsReady
✓ DriveFormat
✓ RootDirectory

Important Method:

✓ DriveInfo.GetDrives()

Common Uses:

✓ Disk Monitoring
✓ Storage Reporting
✓ Backup Applications
✓ Server Health Checks
✓ File Upload Validation
```

# Memory Trick

```text
DriveInfo → Drive Level Information

DirectoryInfo → Folder Level Information

FileInfo → File Level Information
```

Remember:

```text
DriveInfo does not create drives.

It only reads information about existing drives.
```