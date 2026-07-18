# SFTP (Secure File Transfer Protocol):

## What is SFTP?
**SFTP stands for:** Secure File Transfer Protocol

**Used to:**
```text
 Client
    ↓
SFTP Server
```
- Upload Files
- Download Files
- Move Files
- Delete Files
- Read Files

### Why SFTP?

**Normal FTP:**
- Username, Password, Data sent as plain text.
- Not secure.

**`SFTP:`**
- Username, Password, Data encrypted using:
- over SSH


## SFTP vs FTP

| FTP | SFTP |
|-------|-------|
| Not Secure | Secure |
| Port 21 | Port 22 |
| Plain Text | Encrypted |
| Uses FTP Protocol | Uses SSH Protocol |


## SFTP Architecture

```text
Application
      ↓
SFTP Client
      ↓
SSH Channel
      ↓
SFTP Server
      ↓
Remote Files
```

---

## Common Information Required:
- Host Name
- Port
- User Name
- Password
- SSH Key
- Host Key Fingerprint

**Example:**
```
Host      : sftp.bank.com
Port      : 22
User      : nachuser
Password  : *****
```


## SFTP Operations

### Connect

```text
Client
    ↓
Authentication
    ↓
Connected
```

## Upload File

```text
Local File
      ↓
SFTP Server
```

## Download File

```text
SFTP Server
      ↓
Local System
```


## Delete File

```text
Server File
      ↓
Deleted
```


## Move File

```text
Folder A
      ↓
Folder B
```
---