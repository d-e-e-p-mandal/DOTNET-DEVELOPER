# ByteArrayContent
- `ByteArrayContent` is a class in .NET that is used to **send binary data (byte array)** in an HTTP request.
- It inherits from `HttpContent`.

It is commonly used to send:
- Images
- PDF files
- Audio files
- Video files
- Binary files

### Namespace

```csharp
using System.Net.Http;
```

## Set Content Type
- Always specify the correct content type.

```csharp
content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue(
        "application/octet-stream");
```

## Content Types

| Content Type | Purpose |
|--------------|---------|
| application/octet-stream | Generic binary data |
| image/png | PNG image |
| image/jpeg | JPEG image |
| application/pdf | PDF document |
| application/zip | ZIP file |
| audio/mpeg | MP3 audio |
| video/mp4 | MP4 video |

---


**Why Do We Need ByteArrayContent?**
- Some data cannot be represented as text.

For example:
- JPG Image
- PNG Image
- PDF Document
- ZIP File

- These files are stored as **bytes** in memory.
- `ByteArrayContent` is used to send these bytes to a web server.

**How It Works:**
```text
Application
      │
      ▼
    byte[]
      │
      ▼
ByteArrayContent
      │
      ▼
  HttpClient
      │
      ▼
  Web Server
```

---

## Inheritance

```text
HttpContent
      ▲
      │
ByteArrayContent
```

`ByteArrayContent` inherits from `HttpContent`.


# Create ByteArrayContent

```csharp
byte[] data = new byte[]
{
    10,
    20,
    30,
    40
};

ByteArrayContent content = new ByteArrayContent(data);
```

## Constructor

```csharp
ByteArrayContent(byte[] content)
```

| Parameter | Description |
|-----------|-------------|
| content | Byte array to send |


## Constructor with Offset and Length
- Sometimes you want to send only part of the byte array.

```csharp
ByteArrayContent(
    byte[] content,
    int offset,
    int count
)
```

**Example:**
```csharp
byte[] data =
{
    10,
    20,
    30,
    40,
    50
};

ByteArrayContent content =
    new ByteArrayContent(
        data,
        1,
        3);
```

Only these bytes are sent:

```text
20
30
40
```

---

### Example 1 - Send Byte Array

```csharp
HttpClient client = new HttpClient();

byte[] data =
{
    10,
    20,
    30,
    40
};

ByteArrayContent content = new ByteArrayContent(data);

await client.PostAsync("https://example.com/api/data", content);
```

### Example 2 - Send an Image
```csharp
HttpClient client = new HttpClient();
byte[] image = File.ReadAllBytes("photo.jpg");

ByteArrayContent content = new ByteArrayContent(image);
content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue(
        "image/jpeg");

await client.PostAsync("https://example.com/api/upload", content);
```

### Example 3 - Send a PDF
```csharp
HttpClient client = new HttpClient();
byte[] pdf = File.ReadAllBytes("document.pdf");

ByteArrayContent content = new ByteArrayContent(pdf);

content.Headers.ContentType =
    new System.Net.Http.Headers.MediaTypeHeaderValue("application/pdf");

await client.PostAsync("https://example.com/api/upload", content);
```

---

### Data Flow
```text
File
   │
   ▼
byte[]
   │
   ▼
ByteArrayContent
   │
   ▼
HttpClient
   │
   ▼
Server
```

---

# Properties

`ByteArrayContent` inherits properties from `HttpContent`.

| Property | Description |
|----------|-------------|
| Headers | Gets the content headers |

Example

```csharp
Console.WriteLine(content.Headers.ContentType);
```

Output

```text
image/jpeg
```

---

# Advantages

- Simple to use.
- Supports all binary data.
- Efficient for small and medium-sized binary files.
- Integrates directly with `HttpClient`.

---

# Limitations

- Stores the entire byte array in memory.
- Not suitable for very large files.
- Large files can increase memory usage.

---

# When Should You Use ByteArrayContent?

Use `ByteArrayContent` when sending:

- Images
- PDF files
- ZIP files
- Binary files
- Audio files
- Video files

Do **not** use it for very large files. In those cases, `StreamContent` is usually a better choice.

---

# Best Practices

- Set the correct **Content-Type**.
- Use `ByteArrayContent` for small or medium-sized binary files.
- For large files, prefer `StreamContent`.
- Dispose of the content when it is no longer needed if it is not managed automatically.

---

# Interview Questions

### 1. What is ByteArrayContent?

`ByteArrayContent` is a class used to send **binary data stored in a byte array** in an HTTP request.

---

### 2. Which class does ByteArrayContent inherit from?

`HttpContent`.

---

### 3. Which data types are commonly sent using ByteArrayContent?

- Images
- PDF files
- ZIP files
- Audio files
- Video files

---

### 4. Why should you set the Content-Type header?

It tells the server what type of binary data is being sent.

---

### 5. When should you use StreamContent instead?

When sending **large files**, because it streams the data instead of loading the entire file into memory.

---

# ByteArrayContent vs StringContent

| ByteArrayContent | StringContent |
|------------------|---------------|
| Sends binary data | Sends text data |
| Uses `byte[]` | Uses `string` |
| Used for images, PDFs, ZIP files | Used for JSON, XML, HTML, plain text |
| Best for binary files | Best for text-based content |

---
