# FormUrlEncodedContent
- `FormUrlEncodedContent` is a class in .NET that is used to send **HTML form data** in an HTTP request.

- It inherits from `HttpContent`.
- The data is sent in **key-value pair** format.

It is commonly used for:
- Login Forms
- Registration Forms
- Search Forms
- Contact Forms
- OAuth Token Requests
- Web APIs that accept form data


### Namespace
```csharp
using System.Net.Http;
```

**Why Do We Need FormUrlEncodedContent?**
Many web applications and APIs expect data in **HTML form format** instead of JSON.

**Example Form:**
```text
Username : john
Password : 12345
```

The browser sends it as:
```text
username=john&password=12345
```
- `FormUrlEncodedContent` automatically converts key-value pairs into this format.

---

### How It Works

```text
Application
      │
      ▼
Key-Value Pairs
      │
      ▼
FormUrlEncodedContent
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
FormUrlEncodedContent
```

`FormUrlEncodedContent` inherits from `HttpContent`.

---

## Data Format
**Suppose we have:**
| Key | Value |
|-----|-------|
| username | john |
| password | 12345 |

It is converted into:

```text
username=john&password=12345
```

If values contain spaces or special characters, they are automatically URL encoded.

Example

```text
Name = John Doe
```

becomes

```text
Name=John%20Doe
```

---

## Create FormUrlEncodedContent

```csharp
var data = new Dictionary<string, string>
{
    { "username", "john" },
    { "password", "12345" }
};

FormUrlEncodedContent content = new FormUrlEncodedContent(data);
```

---

## Constructor

```csharp
FormUrlEncodedContent(IEnumerable<KeyValuePair<string, string>> nameValueCollection)
```

| Parameter | Description |
|-----------|-------------|
| nameValueCollection | Collection of key-value pairs |

---

## Content Type

`FormUrlEncodedContent` automatically sets the content type.
```text
application/x-www-form-urlencoded
```

You do **not** need to set it manually.

---

# Example 1 - Login Form

```csharp
HttpClient client = new HttpClient();

var loginData = new Dictionary<string, string>
{
    { "username", "john" },
    { "password", "12345" }
};

FormUrlEncodedContent content = new FormUrlEncodedContent(loginData);

await client.PostAsync("https://example.com/login", content);
```

---

# Example 2 - Registration Form

```csharp
HttpClient client = new HttpClient();

var formData = new Dictionary<string, string>
{
    { "firstName", "John" },
    { "lastName", "Doe" },
    { "email", "john@example.com" }
};

FormUrlEncodedContent content = new FormUrlEncodedContent(formData);

await client.PostAsync("https://example.com/register", content);
```

---

# Example 3 - OAuth Token Request

Many OAuth servers require form-urlencoded data.

```csharp
HttpClient client = new HttpClient();

var tokenData = new Dictionary<string, string>
{
    { "grant_type", "password" },
    { "username", "john" },
    { "password", "12345" }
};

FormUrlEncodedContent content = new FormUrlEncodedContent(tokenData);

await client.PostAsync("https://example.com/token", content);
```

---

# Data Flow

```text
Dictionary<string, string>
           │
           ▼
FormUrlEncodedContent
           │
           ▼
HttpClient
           │
           ▼
Server
```

---

## Properties

- `FormUrlEncodedContent` inherits properties from `HttpContent`.
| Property | Description |
|----------|-------------|
| Headers | Gets the content headers |

Example

```csharp
Console.WriteLine(content.Headers.ContentType);
```

Output

```text
application/x-www-form-urlencoded
```

---

# Advantages

- Easy to send HTML form data.
- Automatically URL encodes values.
- Automatically sets the correct content type.
- Simple to use with `HttpClient`.
- Ideal for web forms and OAuth requests.

---

# Limitations

- Supports only text-based key-value pairs.
- Cannot upload files.
- Not suitable for JSON or XML payloads.
- Cannot directly send binary data.

---

# When Should You Use FormUrlEncodedContent?

Use `FormUrlEncodedContent` when:

- Submitting login forms.
- Sending registration data.
- Calling OAuth token endpoints.
- Sending simple key-value form data.

Do **not** use it for:

- JSON requests
- File uploads
- Images
- Videos

---

# Best Practices

- Use meaningful key names.
- Send only text-based values.
- Use HTTPS when sending sensitive data such as passwords.
- Do not use it for file uploads.
- Use `StringContent` when the API expects JSON.

---

# Interview Questions

### 1. What is FormUrlEncodedContent?

`FormUrlEncodedContent` is a class used to send **form data as URL-encoded key-value pairs** in an HTTP request.

---

### 2. Which class does FormUrlEncodedContent inherit from?

`HttpContent`.

---

### 3. Which content type does FormUrlEncodedContent use?

```text
application/x-www-form-urlencoded
```

---

### 4. What type of data does FormUrlEncodedContent send?

Text-based **key-value pairs**.

---

### 5. Can FormUrlEncodedContent upload files?

No.

For file uploads, use `MultipartFormDataContent`.

---

# FormUrlEncodedContent vs StringContent

| FormUrlEncodedContent | StringContent |
|------------------------|---------------|
| Sends key-value form data | Sends plain text, JSON, XML, or HTML |
| Uses `Dictionary<string, string>` | Uses `string` |
| Content-Type is `application/x-www-form-urlencoded` | Content-Type depends on what you specify (e.g., `application/json`) |
| Commonly used for HTML forms and OAuth | Commonly used for REST APIs with JSON |

---
