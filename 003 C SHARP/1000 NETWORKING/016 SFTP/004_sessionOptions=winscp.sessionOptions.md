# SessionOptions (WinSCP.SessionOptions)

## What is SessionOptions?

`SessionOptions` contains all information required to connect to an SFTP server.

Simple Meaning:

```text
Connection Settings Object
```

Before connecting, WinSCP must know:

```text
Which Server?

Which Port?

Which User?

Which Password?

Which Protocol?
```

All this information is stored in:

```cs
WinSCP.SessionOptions
```

---

# Namespace

```cs
using WinSCP;
```

---

# Create SessionOptions

```cs
SessionOptions sessionOptions =
    new SessionOptions();
```

or

```cs
WinSCP.SessionOptions sessionOptions =
    new WinSCP.SessionOptions();
```

---

# Common Properties

## Protocol

### Purpose

Specifies connection protocol.

```cs
sessionOptions.Protocol =
    Protocol.Sftp;
```

Meaning:

```text
Use SFTP Protocol
```

Other Values:

```text
Sftp

Ftp

Scp
```

---

## HostName

### Purpose

Server address.

```cs
sessionOptions.HostName =
    "sftp.bank.com";
```

Meaning:

```text
Which Server To Connect?
```

Example:

```text
sftp.bank.com

192.168.1.10
```

---

## PortNumber

### Purpose

Server port.

```cs
sessionOptions.PortNumber =
    22;
```

Meaning:

```text
Which Port To Connect?
```

Common Ports:

```text
22  → SFTP

21  → FTP

443 → HTTPS
```

---

## UserName

### Purpose

Login user name.

```cs
sessionOptions.UserName =
    "deep";
```

Meaning:

```text
Server Login User
```

---

## Password

### Purpose

Login password.

```cs
sessionOptions.Password =
    "12345";
```

Meaning:

```text
Server Login Password
```

---

## SshHostKeyFingerprint

### Purpose

Verify server identity.

```cs
sessionOptions.SshHostKeyFingerprint =
    "ssh-rsa 2048 xx:xx:xx";
```

Meaning:

```text
Verify Real Server
```

Prevents:

```text
Fake Server

Man-In-The-Middle Attack
```

---

## SshPrivateKeyPath

### Purpose

SSH Key Authentication.

```cs
sessionOptions.SshPrivateKeyPath =
    @"C:\Keys\bank.ppk";
```

Meaning:

```text
Login Using SSH Key
Instead Of Password
```

---

## PrivateKeyPassphrase

### Purpose

Password for SSH key.

```cs
sessionOptions.PrivateKeyPassphrase =
    "mypassword";
```

---

## Timeout

### Purpose

Connection timeout.

```cs
sessionOptions.Timeout =
    TimeSpan.FromMinutes(2);
```

Meaning:

```text
Wait Maximum 2 Minutes
```

---

# Complete Example

```cs
SessionOptions sessionOptions =
    new SessionOptions
    {
        Protocol =
            Protocol.Sftp,

        HostName =
            "sftp.bank.com",

        PortNumber =
            22,

        UserName =
            "deep",

        Password =
            "12345",

        SshHostKeyFingerprint =
            "ssh-rsa 2048 xx:xx:xx"
    };
```

---

# Flow

```text
SessionOptions
      ↓
Contains
      ↓
HostName

PortNumber

UserName

Password

Protocol

HostKey
      ↓
Used By
      ↓
Session.Open()
      ↓
Connected To SFTP Server
```

---

# Real Banking Example

```text
NPCI SFTP Server
        ↓
HostName
        ↓
sftp.npci.org

Port
        ↓
22

User
        ↓
BANK001

Password
        ↓
*****

Protocol
        ↓
SFTP
```

Stored In:

```cs
SessionOptions
```

Then:

```cs
Session session =
    new Session();

session.Open(
    sessionOptions);
```

Result:

```text
Connected To NPCI SFTP Server
```

---

# Quick Revision

```text
SessionOptions
      ↓
Connection Settings

Protocol
      ↓
SFTP / FTP / SCP

HostName
      ↓
Server Address

PortNumber
      ↓
Server Port

UserName
      ↓
Login User

Password
      ↓
Login Password

SshHostKeyFingerprint
      ↓
Verify Server

SshPrivateKeyPath
      ↓
SSH Key Login

Timeout
      ↓
Connection Timeout

Used In
      ↓
session.Open(sessionOptions)
```