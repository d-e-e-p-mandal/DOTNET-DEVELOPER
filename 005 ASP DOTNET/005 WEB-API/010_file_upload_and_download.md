# File Upload API & Download API in ASP.NET Core

---

# 1. File Upload API

## What is File Upload API?

File Upload API is used to upload files from client to server.

---

# Common Uploaded Files

- Images
- PDFs
- Videos
- Documents
- Excel Files
- ZIP Files

---

# Flow of File Upload API

```text
Client Selects File
        ↓
HTTP Request Sent
        ↓
ASP.NET Core API Receives File
        ↓
Server Saves File
        ↓
Response Returned
```

---

# Important Namespace

```cs
using Microsoft.AspNetCore.Mvc;
```

---

# Important Type

```cs
IFormFile
```

---

# What is IFormFile?

Represents uploaded file.

Used to:
- Read file
- Save file
- Get file information

---

# Important Properties of IFormFile

| Property | Purpose |
|---|---|
| FileName | Uploaded file name |
| Length | File size |
| ContentType | MIME type |
| Name | Input field name |

---

# Basic File Upload API

```cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class FileController : ControllerBase
{
    [HttpPost("upload")]
    public async Task<IActionResult> Upload(
        IFormFile file)
    {
        // File Path
        var path =
            Path.Combine("Uploads", file.FileName);

        // Save File
        using var stream =
            new FileStream(path, FileMode.Create);

        await file.CopyToAsync(stream);

        return Ok("File Uploaded Successfully");
    }
}
```

---

# Explanation

---

# [HttpPost("upload")]

```cs
[HttpPost("upload")]
```

Creates POST API.

URL:

```text
/api/file/upload
```

---

# IFormFile file

```cs
IFormFile file
```

Receives uploaded file.

---

# Path.Combine()

```cs
Path.Combine("Uploads", file.FileName);
```

Creates file path.

---

# Example

```text
Uploads/image.png
```

---

# FileStream

```cs
new FileStream(path, FileMode.Create)
```

Creates file on server.

---

# CopyToAsync()

```cs
await file.CopyToAsync(stream);
```

Copies uploaded file data into server file.

---

# Return Response

```cs
return Ok("File Uploaded Successfully");
```

Returns success message.

---

# Upload Folder Structure

```text
Project
│
├── Uploads/
│     ├── image.png
│     ├── pdf.pdf
│
├── Controllers/
│
└── Program.cs
```

---

# Request Type

File upload requires:

```text
multipart/form-data
```

---

# Postman File Upload

## Method

```text
POST
```

---

# URL

```text
https://localhost:5001/api/file/upload
```

---

# Body

```text
form-data
```

---

# Key Type

```text
File
```

---

# Example

| Key | Type | Value |
|---|---|---|
| file | File | image.png |

---

# File Upload Validation

---

# Check Null File

```cs
if (file == null)
{
    return BadRequest("File Not Found");
}
```

---

# Check File Size

```cs
if (file.Length > 5 * 1024 * 1024)
{
    return BadRequest("File Too Large");
}
```

---

# Check File Extension

```cs
var extension =
    Path.GetExtension(file.FileName);

if (extension != ".png")
{
    return BadRequest("Only PNG Allowed");
}
```

---

# Upload Multiple Files

## Using List<IFormFile>

```cs
[HttpPost("multiple")]
public async Task<IActionResult> UploadMultiple(
    List<IFormFile> files)
{
    foreach (var file in files)
    {
        var path =
            Path.Combine("Uploads", file.FileName);

        using var stream =
            new FileStream(path, FileMode.Create);

        await file.CopyToAsync(stream);
    }

    return Ok("Files Uploaded");
}
```

---

# Upload File with Model

```cs
public class EmployeeDTO
{
    public string Name { get; set; }

    public IFormFile Image { get; set; }
}
```

---

# API

```cs
[HttpPost]
public async Task<IActionResult> Create(
    [FromForm] EmployeeDTO dto)
{

}
```

---

# Why [FromForm] Used?

Because files come from:

```text
multipart/form-data
```

---

# Static File Access

To access uploaded files from browser:

---

# Program.cs

```cs
app.UseStaticFiles();
```

---

# Save in wwwroot

```text
wwwroot/uploads
```

---

# Example File URL

```text
https://localhost:5001/uploads/image.png
```

---

# Common Upload Problems

| Problem | Reason |
|---|---|
| File null | Wrong form-data |
| File not saving | Folder missing |
| 404 Error | Static files disabled |
| Large file error | Size limit exceeded |

---

# 2. Download API

## What is Download API?

Download API sends files from server to client.

---

# Flow of Download API

```text
Client Requests File
        ↓
Server Reads File
        ↓
File Sent To Client
        ↓
Browser Downloads File
```

---

# Basic Download API

```cs
using Microsoft.AspNetCore.Mvc;

[ApiController]
[Route("api/[controller]")]
public class FileController : ControllerBase
{
    [HttpGet("download")]
    public IActionResult Download()
    {
        var path =
            Path.Combine("Uploads", "sample.pdf");

        var bytes =
            System.IO.File.ReadAllBytes(path);

        return File(
            bytes,
            "application/pdf",
            "sample.pdf"
        );
    }
}
```

---

# Explanation

---

# ReadAllBytes()

```cs
System.IO.File.ReadAllBytes(path);
```

Reads file data into byte array.

---

# File()

```cs
return File(...)
```

Returns downloadable file.

---

# Parameters of File()

| Parameter | Purpose |
|---|---|
| bytes | File data |
| contentType | MIME type |
| fileName | Download file name |

---

# Common MIME Types

| File Type | MIME Type |
|---|---|
| PDF | application/pdf |
| PNG | image/png |
| JPG | image/jpeg |
| TXT | text/plain |
| ZIP | application/zip |

---

# Download URL

```text
https://localhost:5001/api/file/download
```

---

# Browser Result

```text
sample.pdf downloaded
```

---

# Download Image API

```cs
[HttpGet("image")]
public IActionResult GetImage()
{
    var path =
        Path.Combine("Uploads", "photo.png");

    var bytes =
        System.IO.File.ReadAllBytes(path);

    return File(bytes, "image/png");
}
```

---

# Download Using PhysicalFile()

```cs
[HttpGet]
public IActionResult Download()
{
    var path =
        Path.Combine(
            Directory.GetCurrentDirectory(),
            "Uploads/sample.pdf");

    return PhysicalFile(
        path,
        "application/pdf",
        "sample.pdf");
}
```

---

# Difference

| Method | Purpose |
|---|---|
| File() | Byte array download |
| PhysicalFile() | Direct physical file |

---

# File Download Validation

## Check File Exists

```cs
if (!System.IO.File.Exists(path))
{
    return NotFound();
}
```

---

# Complete Download API

```cs
[HttpGet("{fileName}")]
public IActionResult Download(string fileName)
{
    var path =
        Path.Combine("Uploads", fileName);

    if (!System.IO.File.Exists(path))
    {
        return NotFound("File Not Found");
    }

    var bytes =
        System.IO.File.ReadAllBytes(path);

    return File(
        bytes,
        "application/octet-stream",
        fileName
    );
}
```

---

# Security Best Practices

## File Upload Security

- Validate extension
- Validate file size
- Use unique file names
- Store outside root if needed

---

# Dangerous File Types

Avoid:
- .exe
- .bat
- .js

---

# Generate Unique File Name

```cs
var fileName =
    Guid.NewGuid().ToString()
    + Path.GetExtension(file.FileName);
```

---

# Complete Upload Flow

```text
Client Selects File
        ↓
POST Request Sent
        ↓
API Receives File
        ↓
Validation
        ↓
Save File
        ↓
Success Response
```

---

# Complete Download Flow

```text
Client Requests File
        ↓
API Finds File
        ↓
Reads File
        ↓
Returns File Response
        ↓
Browser Downloads File
```

---

# File Upload vs Download

| Upload API | Download API |
|---|---|
| Client → Server | Server → Client |
| Uses IFormFile | Uses File() |
| POST Request | GET Request |
| Saves file | Sends file |

---

# Real-Life Analogy

| ASP.NET Core Feature | Real Life |
|---|---|
| Upload API | Submitting documents |
| Download API | Receiving documents |
| IFormFile | Uploaded package |
| FileStream | Storage box |
| File() | Delivery system |