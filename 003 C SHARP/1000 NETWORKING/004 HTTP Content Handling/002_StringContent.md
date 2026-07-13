# StringContent
- `StringContent` is a class in .NET that is used to **send text data** in an HTTP request.
- It inherits from `HttpContent`.

It is commonly used to send:
- JSON
- XML
- Plain Text
- HTML


### Namespace
```csharp
using System.Net.Http;
using System.Text;
```

**Why Do We Need StringContent?**
- When sending data to a server, the server expects the request body to contain data.
- If the data is in **string format**, such as JSON or XML, we use `StringContent`.
 
**Example JSON:**
```json
{
    "name": "John",
    "age": 25
}
``` 
- The above JSON is a **string**, so it is sent using `StringContent`.

**How It Works:**
```text
Application
      │
      ▼
String Data
      │
      ▼
StringContent
      │
      ▼
HttpClient
      │
      ▼
Web Server
```

---

### Inheritance

```text
HttpContent
      ▲
      │
StringContent
```

`StringContent` inherits from `HttpContent`.

---

### Create StringContent
```csharp
StringContent content = new StringContent("Hello World");
```
- This creates a request body containing:

```text
Hello World
```

---

### Constructor
```csharp
StringContent(string content)
```

| Parameter | Description |
|-----------|-------------|
| content | The string data to send |


### Constructor with Encoding
```csharp
StringContent(string content, Encoding encoding)
```

**Example:**
```csharp
StringContent content = new StringContent("Hello World", Encoding.UTF8);
```

# Constructor with Content Type
```csharp
StringContent(
    string content,
    Encoding encoding,
    string mediaType
)
```

**Example:**
```csharp
StringContent content =
    new StringContent(
        "{ \"name\":\"John\" }",
        Encoding.UTF8,
        "application/json");
```


### Constructor Parameters

| Parameter | Description |
|-----------|-------------|
| content | Text to send |
| encoding | Character encoding (UTF-8, ASCII, etc.) |
| mediaType | Content type (MIME type) |


### Common Content Types
| Content Type | Purpose |
|--------------|---------|
| application/json | JSON Data |
| application/xml | XML Data |
| text/plain | Plain Text |
| text/html | HTML Content |

---

## Example 1 - Send Plain Text

```csharp
HttpClient client = new HttpClient();

StringContent content =
    new StringContent(
        "Hello World",
        Encoding.UTF8,
        "text/plain");

await client.PostAsync("https://example.com/api/message", content);
```

---

## Example 2 - Send JSON
```csharp
using System.Text;
HttpClient client = new HttpClient();

string json =
@"{
    ""name"": ""John"",
    ""age"": 25
}";

StringContent content =
    new StringContent(
        json,
        Encoding.UTF8,
        "application/json");

await client.PostAsync("https://example.com/api/users", content);
```


## Example 3 - Send XML
```csharp
using System.Text;

HttpClient client = new HttpClient();

string xml =
@"<User>
    <Name>John</Name>
    <Age>25</Age>
</User>";

StringContent content =
    new StringContent(
        xml,
        Encoding.UTF8,
        "application/xml");

await client.PostAsync("https://example.com/api/users", content);
```

---

### Data Flow
```text
String
   │
   ▼
StringContent
   │
   ▼
HttpClient
   │
   ▼
Server
```

---

## Properties

`StringContent` inherits properties from `HttpContent`.

| Property | Description |
|----------|-------------|
| Headers | Gets the content headers |

**Example:**
```csharp
Console.WriteLine(content.Headers.ContentType);
```

**Output**
```text
application/json; charset=utf-8
```

---

# Advantages

- Easy to use.
- Perfect for sending JSON and XML.
- Supports multiple text encodings.
- Supports different content types.
- Integrates directly with `HttpClient`.

---

# Limitations

- Only suitable for **text-based data**.
- Not recommended for large files.
- Not suitable for binary data such as images or PDFs.

---

# When Should You Use StringContent?

Use `StringContent` when sending:

- JSON
- XML
- HTML
- Plain text

Do **not** use it for:

- Images
- Videos
- PDF files
- Large binary files

---

# Best Practices

- Use **UTF-8** encoding unless another encoding is required.
- Always specify the correct **Content-Type**.
- Validate JSON or XML before sending.
- Use `application/json` when sending JSON data.
- Keep request bodies as small as practical.

---

# Interview Questions

### 1. What is StringContent?

`StringContent` is a class used to send **string-based data** in an HTTP request.

---

### 2. Which class does StringContent inherit from?

`HttpContent`.

---

### 3. Which types of data can StringContent send?

- JSON
- XML
- Plain Text
- HTML

---

### 4. Why do we specify `"application/json"`?

It tells the server that the request body contains **JSON** data.

---

### 5. Which encoding is commonly used with StringContent?

`Encoding.UTF8`.

---

# StringContent vs HttpContent

| StringContent | HttpContent |
|---------------|-------------|
| Concrete class | Abstract class |
| Can be instantiated | Cannot be instantiated |
| Used for text-based data | Base class for all HTTP content |
| Inherits from `HttpContent` | Parent class |

---