# WinSCP SFTP 

### What is WinSCP?

- **WinSCP stands for:** Windows Secure Copy  
- It is a library/software used to communicate with:
    - SFTP Server
    - FTP Server
    - SCP Server
    - WebDAV Server


**In .NET projects, WinSCP is mostly used for:**
- Upload Files
- Download Files
- Move Files
- Rename Files
- Delete Files
- Check File Exists

### Real World Example

**Suppose your application generates:**
- ACH File
- NACH File
- Report File
- Settlement File. 

Then It needs to send it to a bank server.

**Flow:**

```text
Your Application
        ↓
WinSCP
        ↓
SFTP Server
        ↓
Bank Server
```


### How SFTP Connection Works
- Before transferring files, WinSCP must connect to the SFTP server.

**To connect, it needs:**
- Server Name
- Port Number
- Username
- Password
- Host Key

**Example:**
```text
Host Name : sftp.bank.com
Port      : 22
User Name : deep
Password  : *****
Protocol  : SFTP
```

---

## Step 1 : Create SessionOptions

### What is SessionOptions?

- `SessionOptions` contains all server connection details.

**Simple Meaning:** Connection Configuration Object

**Example:**

```cs
SessionOptions sessionOptions = new SessionOptions
    {
        Protocol = Protocol.Sftp,
        HostName = "sftp.bank.com",
        PortNumber = 22,
        UserName = "deep",
        Password = "12345",
        SshHostKeyFingerprint = "ssh-rsa 2048 xx:xx:xx"
    };
```

### Understanding Each Property

### Protocol
```cs
Protocol = Protocol.Sftp
```

**Meaning:** 
- Which Protocol To Use?

**Possible Values:**
- SFTP
- FTP
- SCP

---

### HostName

```cs
HostName = "sftp.bank.com"
```

**Meaning:**
- Which Server To Connect?

**Example:**
```text
sftp.bank.com

10.20.30.40
```

---

### PortNumber

```cs
PortNumber = 22
```

**Meaning:**
- Which Port To Connect?

**Common Ports:**
- 22  → SFTP
- 21  → FTP
- 443 → HTTPS
---

### UserName

UserName = "deep"
**Meaning:** Login User

```cs
UserName = "deep",
```

### Password

```cs
Password = "12345"
```

**Meaning:**

```text
User Password
```

### SshHostKeyFingerprint

```cs
SshHostKeyFingerprint = "ssh-rsa 2048 xx:xx:xx"
```

**Meaning:**
- Verify Server Identity


**Purpose:**
- Prevent Fake Servers
- Prevent Man-In-The-Middle Attack

---

## Step 2 : Create Session

### What is Session?
- `Session` represents the actual connection.

**Example:**
```cs
Session session = new Session();
```

**Meaning:** Create Empty Connection Object

**Current State:** Not Connected

## Step 3 : Open Connection

**Example:**
```cs
session.Open(sessionOptions);
```

**What Happens?**
```text
Read Host Name
        ↓
Read Port
        ↓
Read User Name
        ↓
Read Password
        ↓
Connect To Server
        ↓
Verify Host Key
        ↓
Authentication Success
        ↓
Connection Established
```

**Now:** Connected To SFTP Server

### Visual Connection Flow

```text
  SessionOptions
        ↓
    Session
        ↓
      Open()
        ↓
   SFTP Server
        ↓
    Connected
```

---

## Step 4 : Upload File

### PutFiles()
- Used to upload local files to the server.

**Example:**
```cs
session.PutFiles(@"C:\Files\Test.txt", "/upload/");
```

**Flow:**
```text
  Local Machine
        ↓
C:\Files\Test.txt
        ↓
      Upload
        ↓
   Server Folder
        ↓
    /upload/
```

---

### Upload Result

Example:

```cs
TransferOperationResult result = session.PutFiles(@"C:\Files\Test.txt", "/upload/");
```

---

#### Why Result?
- Because upload can fail.

**Example:**
- Server Down
- Network Failure
- Wrong Folder
- Permission Issue

**Check Result:**

```cs
result.Check();
```

**Meaning:**
```text
If Upload Failed
      ↓
Throw Exception

If Upload Success
      ↓
Continue
```


### Upload Multiple Files

### Upload All TXT Files

```cs
session.PutFiles(@"C:\Files\*.txt", "/upload/");
```

**Uploads:**
- A.txt
- B.txt
- C.txt

---

### Upload All XML Files

```cs
session.PutFiles(@"C:\Files\*.xml", "/upload/");
```

**Uploads:**
- A.xml
- B.xml
- C.xml

### Upload Everything

```cs
session.PutFiles(@"C:\Files\*", "/upload/");
```

**Uploads:**
- All Files


### Upload Multiple Selected Files

**Suppose:**
- A.txt
- B.txt
- C.txt

**Only upload:**
- A.txt
- C.txt

**Code:**
```cs
string[] files =
{
    @"C:\Files\A.txt",
    @"C:\Files\C.txt"
};

foreach(string file in files)
{
    session.PutFiles(file, "/upload/");
}
```

**Flow:**

```text
A.txt
  ↓
Upload

C.txt
  ↓
Upload
```

---

## Step 5 : Download File

## GetFiles()

Used to download files from server.

Example:

```cs
session.GetFiles("/upload/Test.txt", @"C:\Download\");
```

**Flow:**
```text
   Server
     ↓
  Test.txt
     ↓
  Download
     ↓
C:\Download\
```

---

### Download Multiple Files

```cs
session.GetFiles(
    "/upload/*.txt",
    @"C:\Download\");
```

**Downloads:**
- A.txt
- B.txt
- C.txt

---

## Step 6 : Check File Exists

Example:

```cs
bool exists = session.FileExists("/upload/Test.txt");
```

**Output:**
- true/false


**Used Before:** 
- Alreday Downloaded
- or IF exist then Delete/Move Old File.
 
---

## Step 7 : List Files

**Example:**
```cs
RemoteDirectoryInfo dir = session.ListDirectory("/upload");
```

**Get Files:**
```cs
foreach(RemoteFileInfo file in dir.Files)
{
    Console.WriteLine(file.Name);
}
```

**Output:**
- A.txt
- B.txt
- C.txt

---

## Step 8 : Delete File

**Example:**
```cs
session.RemoveFiles("/upload/Test.txt");
```

**Flow:**
```text
Server File
      ↓
Delete
      ↓
Removed
```

---

## Step 9 : Move/Rename File

**Rename:**

```cs
session.MoveFile("/upload/Test.txt", "/upload/Test1.txt");
```

**Flow:**
```text
Test.txt
      ↓
Test1.txt
```

## Move To Another Folder

```cs
session.MoveFile(
    "/upload/Test.txt",
    "/archive/Test.txt");
```

**Flow:**
```text
Upload Folder
      ↓
Archive Folder
```

---

## Real World Example: Complete Banking Flow

### Outward ACH File

```text
Generate ACH File
        ↓
ACH_001.txt
        ↓
Create SessionOptions
        ↓
Create Session
        ↓
Open Connection
        ↓
Upload ACH File
        ↓
NPCI SFTP Server
```

---

## Inward Response File

```text
Connect To SFTP
        ↓
Check Response Folder
        ↓
Download RES File
        ↓
Save To Local Folder
        ↓
Process Database
```

---

# Complete Lifecycle

```text
Create SessionOptions
          ↓
Create Session
          ↓
Open Connection
          ↓
Upload File
          ↓
Download File
          ↓
Move File
          ↓
Delete File
          ↓
Close Connection
```

---

## Most Important Classes


### SessionOptions
**Purpose:** Connection Settings


### Session
**Purpose:** SFTP Connection


### TransferOperationResult


**Purpose:** Upload/Download Result



### TransferOptions
**Purpose:** Transfer Configuration


### RemoteDirectoryInfo
**Purpose:** Directory Information

### RemoteFileInfo
**Purpose:** File Information