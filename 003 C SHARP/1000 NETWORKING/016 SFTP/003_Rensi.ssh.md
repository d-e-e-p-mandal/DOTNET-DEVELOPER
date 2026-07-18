# SSH.NET (Renci.SshNet) Complete Notes

### What is SSH.NET?
SSH.NET is a .NET library used for:
- SSH
- SFTP
- SCP
- Remote Command Execution


**NuGet Package:**
```text
SSH.NET
```

**Namespace:**
```cs
using Renci.SshNet;
```

---

## Why Use SSH.NET?

**Used to:**
- Connect To SFTP Server
- Upload Files
- Download Files
- Delete Files
- Move Files
- Read Directories
- Execute Linux Commands

---

## SSH.NET vs WinSCP

| WinSCP | SSH.NET |
|----------|----------|
| Easy To Use | More Flexible |
| File Transfer Focused | Full SSH Support |
| Requires WinSCP DLL | Pure .NET Library |
| Banking Projects | Banking Projects |
| SFTP Operations | SFTP + SSH Commands |

---

# Main Classes

## SftpClient

Purpose:

```text
SFTP Operations
```

**Used For:**
- Upload
- Download
- Delete
- Rename
- List Files

---

## ScpClient

**Purpose:**
- SCP File Transfer



## SshClient

**Purpose:**
- Execute Linux Commands


## ConnectionInfo

**Purpose:**
- Connection Configuration


Contains:
- Host
- Port
- Username
- Password
- SSH Key


---

## SftpClient

## What is SftpClient?
- Represents SFTP connection.

Example:

```cs
SftpClient client = new SftpClient(
        "sftp.bank.com",
        "user",
        "password");
```

---

# Connection Flow

```text
Create SftpClient
        ↓
Connect()
        ↓
Connected
        ↓
Upload / Download
        ↓
Disconnect()
```

---

# Connect()

## Purpose

Connect to SFTP server.

Example:

```cs
client.Connect();
```

---

## Check Connection

```cs
client.IsConnected
```

Output:

```text
true

false
```

---

# Disconnect()

## Purpose

Close connection.

Example:

```cs
client.Disconnect();
```

---

# Upload File

## UploadFile()

Purpose:

```text
Upload Local File
To Server
```

Example:

```cs
using var file = File.OpenRead(@"C:\Files\Test.txt");

client.UploadFile(
    file,
    "/upload/Test.txt");
```

---

## Flow

```text
Local File
      ↓
UploadFile()
      ↓
SFTP Server
```

---

## Upload Multiple Files

Example:

```cs
string[] files =
{
    @"C:\Files\A.txt",
    @"C:\Files\B.txt",
    @"C:\Files\C.txt"
};

foreach(string filePath in files)
{
    using var file = File.OpenRead(filePath);

    client.UploadFile(
        file,
        "/upload/" +
        Path.GetFileName(filePath));
}
```

---

## Upload All Files From Folder

```cs
foreach(string file in Directory.GetFiles(@"C:\Files"))
{
    using var stream = File.OpenRead(file);

    client.UploadFile(
        stream,
        "/upload/" +
        Path.GetFileName(file));
}
```

---

# Download File

## DownloadFile()

Purpose:

```text
Download Server File
```

Example:

```cs
using var file = File.Create(
        @"C:\Files\Test.txt");

client.DownloadFile(
    "/upload/Test.txt",
    file);
```

---

## Flow

```text
Server File
      ↓
DownloadFile()
      ↓
Local File
```

---

# Download Multiple Files

```cs
foreach(var file in client.ListDirectory(
        "/upload"))
{
    if(file.IsDirectory)
        continue;

    using var stream =
        File.Create(
            @"C:\Download\" +
            file.Name);

    client.DownloadFile(
        file.FullName,
        stream);
}
```

---

## Delete File

## DeleteFile()

Example:

```cs
client.DeleteFile(
    "/upload/Test.txt");
```

---

## Rename File

## RenameFile()

Example:

```cs
client.RenameFile(
    "/upload/Test.txt",
    "/upload/Test1.txt");
```

---

# Move File

Example:

```cs
client.RenameFile(
    "/upload/Test.txt",
    "/archive/Test.txt");
```

---

# Check File Exists

Example:

```cs
bool exists = client.Exists("/upload/Test.txt");
```

Output:

```text
true

false
```

---

# Create Directory

## CreateDirectory()

Example:

```cs
client.CreateDirectory("/archive");
```

---

## Delete Directory

## DeleteDirectory()

Example:

```cs
client.DeleteDirectory("/archive");
```

---

# List Directory

## ListDirectory()

Example:

```cs
var files = client.ListDirectory("/upload");
```

---

## Loop Files

```cs
foreach(var file in files)
{
    Console.WriteLine(file.Name);
}
```

---

# SftpFile

## What is SftpFile?

Represents file information.

Obtained From:

```cs
ListDirectory()
```

---

## Common Properties

```cs
file.Name

file.FullName

file.Length

file.LastWriteTime

file.IsDirectory

file.IsRegularFile
```

---

# Execute Linux Commands

# SshClient

Purpose:

```text
Execute Commands
On Linux Server
```

---

## Example

```cs
using var ssh = new SshClient(
        "server",
        "user",
        "password");

ssh.Connect();
```

---

## Execute Command

```cs
var result = ssh.RunCommand("ls -la");
```

---

## Output

```cs
Console.WriteLine(result.Result);
```

---

# Common Linux Commands

- ls
- pwd
- mkdir
- rm
- mv
- cat
- top

---

# SSH Key Authentication

## Why?

- Instead of password.

- More Secure.

---

## Private Key File

```text
bank.ppk

id_rsa
```

---

## Example

```cs
PrivateKeyFile key = new PrivateKeyFile(@"C:\Keys\id_rsa");
```

---

```cs
SftpClient client = new SftpClient(
        "server",
        "user",
        key);
```

---

# ConnectionInfo

## What is ConnectionInfo?

- Stores complete connection details.

**Example:**

```cs
ConnectionInfo info = new ConnectionInfo(
        "sftp.bank.com",
        22,
        "user",
        new PasswordAuthenticationMethod(
            "user",
            "password"));
```

---

## Use

```cs
SftpClient client = new SftpClient(info);
```

---

# Complete Upload Example

```cs
using Renci.SshNet;

using var client =
    new SftpClient(
        "sftp.bank.com",
        "user",
        "password");

client.Connect();

using var file =
    File.OpenRead(
        @"C:\Files\Test.txt");

client.UploadFile(
    file,
    "/upload/Test.txt");

client.Disconnect();
```

---

# Complete Banking Flow

```text
Background Service
        ↓
Generate ACH File
        ↓
Create SftpClient
        ↓
Connect()
        ↓
UploadFile()
        ↓
Bank SFTP Server
        ↓
Disconnect()
```

---

# Commonly Used Classes

```cs
SftpClient

SshClient

ScpClient

ConnectionInfo

PrivateKeyFile

SftpFile
```

---

# Commonly Used Methods

```cs
Connect()

Disconnect()

UploadFile()

DownloadFile()

DeleteFile()

RenameFile()

Exists()

CreateDirectory()

DeleteDirectory()

ListDirectory()
```

---