# StreamContent
- `StreamContent` is a class in .NET that is used to **send data from a Stream** in an HTTP request.
- It inherits from `HttpContent`.

It is commonly used to send:
- Large files
- Images
- Videos
- Audio files
- PDF files
- Any file that is read as a stream

Unlike `ByteArrayContent`, **StreamContent does not need to load the entire file into memory**.

---

### Namespace
```csharp
using System.Net.Http;
using System.IO;
```


**Why Do We Need StreamContent?**
Suppose you want to upload a **2 GB video**.

If you use `ByteArrayContent`:
```text
Video File
     │
     ▼
Load Entire File into Memory
     │
     ▼
Send to Server
```

- This uses a large amount of memory.

With `StreamContent`:
```text
Video File
     │
     ▼
Read Small Parts (Stream)
     │
     ▼
Send to Server
```

- Only a small portion of the file is kept in memory at a time.


# How It Works

```text
Application
      │
      ▼
FileStream
      │
      ▼
StreamContent
      │
      ▼
HttpClient
      │
      ▼
Web Server
```

---

# Inheritance

```text
HttpContent
      ▲
      │
StreamContent
```

`StreamContent` inherits from `HttpContent`.

---

## Create StreamContent

```csharp
FileStream stream = File.OpenRead("photo.jpg");

StreamContent content = new StreamContent(stream);
```


## Constructor
```csharp
StreamContent(Stream content)
```

| Parameter | Description |
|-----------|-------------|
| content | Stream containing the data to send |


## Constructor with Buffer Size
- You can specify the buffer size used while reading the stream.

```csharp
StreamContent(Stream content, int bufferSize)
```

**Example:**
```csharp
FileStream stream = File.OpenRead("video.mp4");

StreamContent content =
    new StreamContent(
        stream,
        8192);
```

---

## Set Content Type
- Always specify the correct content type.

```csharp
content.Headers.ContentType = new System.Net.Http.Headers.MediaTypeHeaderValue("image/jpeg");
```

---

# Common Content Types

| Content Type | Purpose |
|--------------|---------|
| application/octet-stream | Generic binary file |
| image/jpeg | JPEG image |
| image/png | PNG image |
| application/pdf | PDF document |
| video/mp4 | MP4 video |
| audio/mpeg | MP3 audio |

---

# Example 1 - Upload an Image

```csharp
HttpClient client = new HttpClient();

using FileStream stream = File.OpenRead("photo.jpg");

StreamContent content = new StreamContent(stream);

content.Headers.ContentType =
    new System.Net.Http.Headers.MediaTypeHeaderValue(
        "image/jpeg");

await client.PostAsync("https://example.com/api/upload", content);
```

---

# Example 2 - Upload a PDF

```csharp
HttpClient client = new HttpClient();

using FileStream stream = File.OpenRead("document.pdf");

StreamContent content = new StreamContent(stream);

content.Headers.ContentType =
    new System.Net.Http.Headers.MediaTypeHeaderValue(
        "application/pdf");

await client.PostAsync("https://example.com/api/upload", content);
```

---

# Example 3 - Upload a Video

```csharp
HttpClient client = new HttpClient();

using FileStream stream = File.OpenRead("movie.mp4");

StreamContent content = new StreamContent(stream);

content.Headers.ContentType =
    new System.Net.Http.Headers.MediaTypeHeaderValue(
        "video/mp4");

await client.PostAsync("https://example.com/api/upload", content);
```

---

### Data Flow

```text
Large File
     │
     ▼
FileStream
     │
     ▼
StreamContent
     │
     ▼
HttpClient
     │
     ▼
   Server
```

---

# Properties

`StreamContent` inherits properties from `HttpContent`.

| Property | Description |
|----------|-------------|
| Headers | Gets the content headers |

**Example:**

```csharp
Console.WriteLine(content.Headers.ContentType);
```

**Output**
```text
image/jpeg
```

---

# Advantages

- Efficient for large files.
- Uses less memory.
- Streams data while sending.
- Supports all file types.
- Integrates directly with `HttpClient`.

---

# Limitations

- Requires a `Stream` object.
- Slightly more complex than `ByteArrayContent`.
- The stream must remain open until the request is completed.

---

# When Should You Use StreamContent?

Use `StreamContent` when sending:

- Large images
- Large PDF files
- Videos
- Audio files
- Large binary files

Avoid it for small text data. For JSON or XML, use `StringContent`.

---

# Best Practices

- Use `using` to automatically dispose the stream.
- Set the correct **Content-Type**.
- Use `StreamContent` for large files.
- Keep the stream open until the upload is finished.
- Close or dispose the stream after the request completes.

---

# Interview Questions

### 1. What is StreamContent?

`StreamContent` is a class used to send data from a `Stream` in an HTTP request.

---

### 2. Which class does StreamContent inherit from?

`HttpContent`.

---

### 3. Why is StreamContent preferred for large files?

Because it streams the data without loading the entire file into memory.

---

### 4. Which object is required to create a StreamContent?

A `Stream` object, such as a `FileStream`.

---

### 5. Should the stream remain open while uploading?

Yes. The stream must remain open until the HTTP request has finished sending the data.

---

# StreamContent vs ByteArrayContent

| StreamContent | ByteArrayContent |
|---------------|------------------|
| Uses a `Stream` | Uses a `byte[]` |
| Best for large files | Best for small or medium files |
| Low memory usage | Higher memory usage for large files |
| Streams data gradually | Loads the entire byte array into memory |

---