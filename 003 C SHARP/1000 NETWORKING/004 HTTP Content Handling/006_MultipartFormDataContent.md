# MultipartFormDataContent

- `MultipartFormDataContent` is a class in .NET that is used to send **multipart/form-data** in an HTTP request.
- It inherits from `HttpContent`.

It is mainly used for:
- File Upload
- Image Upload
- PDF Upload
- Video Upload
- Sending files along with form fields


### Namespace
```csharp
using System.Net.Http;
using System.IO;
```


**Why Do We Need MultipartFormDataContent?**
- Suppose you have a registration form.

The user enters:
- Name
- Email
- Profile Picture

Here,

- Name → Text
- Email → Text
- Profile Picture → File

`FormUrlEncodedContent` **cannot upload files**.

`MultipartFormDataContent` is designed to send **both text fields and files together**.


### How It Works

```text
Application
      │
      ▼
Text + Files
      │
      ▼
MultipartFormDataContent
      │
      ▼
HttpClient
      │
      ▼
Web Server
```


## Inheritance
```text
HttpContent
      ▲
      │
MultipartFormDataContent
```

`MultipartFormDataContent` inherits from `HttpContent`.


## Content Type
- When using `MultipartFormDataContent`, the request content type is automatically set to:
`multipart/form-data`

You do **not** need to set it manually.

---

## Create MultipartFormDataContent

```csharp
MultipartFormDataContent content = new MultipartFormDataContent();
```

Initially, the content is empty.

You add text fields and files using the `Add()` method.

---

# Add Text Data

```csharp
MultipartFormDataContent content = new MultipartFormDataContent();

content.Add(new StringContent("John"), "name");

content.Add(new StringContent("john@example.com"), "email");
```

---

# Add File

```csharp
FileStream stream = File.OpenRead("photo.jpg");

StreamContent fileContent = new StreamContent(stream);

content.Add(
    fileContent,
    "photo",
    "photo.jpg");
```

---

# Add() Method

```csharp
content.Add(HttpContent content, string name);
```

| Parameter | Description |
|-----------|-------------|
| content | Content to add |
| name | Form field name |

---

# Add() Method for Files

```csharp
content.Add(
    HttpContent content,
    string name,
    string fileName
);
```

| Parameter | Description |
|-----------|-------------|
| content | File content |
| name | Form field name |
| fileName | File name sent to the server |

---

# Example 1 - Upload a Single File

```csharp
HttpClient client = new HttpClient();

using FileStream stream = File.OpenRead("photo.jpg");

StreamContent fileContent = new StreamContent(stream);

MultipartFormDataContent content = new MultipartFormDataContent();

content.Add(
    fileContent,
    "photo",
    "photo.jpg");

await client.PostAsync("https://example.com/api/upload", content);
```

---

# Example 2 - Upload File with Text Fields

```csharp
HttpClient client = new HttpClient();

using FileStream stream = File.OpenRead("resume.pdf");

StreamContent fileContent = new StreamContent(stream);
MultipartFormDataContent content = new MultipartFormDataContent();

content.Add(new StringContent("John"), "name");
content.Add(new StringContent("john@example.com"), "email");

content.Add(
    fileContent,
    "resume",
    "resume.pdf");

await client.PostAsync("https://example.com/api/upload", content);
```

---

# Example 3 - Upload Multiple Files

```csharp
HttpClient client = new HttpClient();

MultipartFormDataContent content = new MultipartFormDataContent();

using FileStream stream1 = File.OpenRead("photo1.jpg");
using FileStream stream2 = File.OpenRead("photo2.jpg");

content.Add(
    new StreamContent(stream1),
    "photos",
    "photo1.jpg");

content.Add(
    new StreamContent(stream2),
    "photos",
    "photo2.jpg");

await client.PostAsync(
    "https://example.com/api/upload",
    content);
```

---

# Data Flow

```text
Text Fields
      │
      ├────────┐
      │        │
      ▼        ▼
StringContent  StreamContent
        │        │
        └────┬───┘
             ▼
MultipartFormDataContent
             │
             ▼
HttpClient
             │
             ▼
Server
```

---

# Properties

`MultipartFormDataContent` inherits properties from `HttpContent`.

| Property | Description |
|----------|-------------|
| Headers | Gets the content headers |

Example

```csharp
Console.WriteLine(
    content.Headers.ContentType);
```

Output

```text
multipart/form-data
```

---

# Advantages

- Uploads one or more files.
- Sends files and text together.
- Automatically creates multipart boundaries.
- Automatically sets the correct content type.
- Works with all file types.

---

# Limitations

- More complex than `StringContent` or `FormUrlEncodedContent`.
- File streams should remain open until the request is completed.
- Large uploads depend on available network bandwidth.

---

# When Should You Use MultipartFormDataContent?

Use `MultipartFormDataContent` when:

- Uploading images.
- Uploading PDF files.
- Uploading videos.
- Uploading documents.
- Sending files together with form fields.

Do **not** use it for:

- Simple JSON requests.
- Simple text-only forms.
- Plain text data.

---

# Best Practices

- Use `using` when working with `FileStream`.
- Use `StreamContent` for files.
- Use `StringContent` for text fields.
- Dispose of streams after the request completes.
- Validate file size and type before uploading.
- Use HTTPS when uploading sensitive files.

---

# Interview Questions

### 1. What is MultipartFormDataContent?

`MultipartFormDataContent` is a class used to send **multipart/form-data**, including files and form fields, in an HTTP request.

---

### 2. Which class does MultipartFormDataContent inherit from?

`HttpContent`.

---

### 3. Which content type does MultipartFormDataContent use?

```text
multipart/form-data
```

---

### 4. Can MultipartFormDataContent upload multiple files?

Yes.

It can upload one or more files in the same request.

---

### 5. Which classes are commonly used together with MultipartFormDataContent?

- `StringContent` (for text fields)
- `StreamContent` (for files)

---

# MultipartFormDataContent vs FormUrlEncodedContent

| MultipartFormDataContent | FormUrlEncodedContent |
|--------------------------|-----------------------|
| Uploads files and text | Sends only text-based key-value pairs |
| Uses `multipart/form-data` | Uses `application/x-www-form-urlencoded` |
| Supports file uploads | Does not support file uploads |
| Can send multiple files | Cannot send files |
| Used for image, PDF, and document uploads | Used for login forms and simple form data |

---