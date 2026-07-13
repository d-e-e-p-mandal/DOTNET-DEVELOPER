## Methods

### GetAsync()
- Used to retrieve data from server.

**HTTP Method:** GET

**Example:**
```cs
HttpResponseMessage response = await client.GetAsync("api/employees");
```

Use Cases:
- Fetch Employee List
- Get User Details
- Read Records

**Return Type:**
```cs
Task<HttpResponseMessage>
```

---

### PostAsync()
- Used to send data to server.

**HTTP Method:** POST

**Example:**
```cs
await client.PostAsync("api/employees", content);
```

**Use Cases:**
- Create Employee
- Register User
- Save Data

**Return Type:**
```cs
Task<HttpResponseMessage>
```

---

### PutAsync()
- Used to update an entire resource.

**HTTP Method:** PUT

**Example:**
```cs
await client.PutAsync("api/employees/1", content);
```

Use Cases:
- Update Employee
- Update Product

**Return Type:**
```cs
Task<HttpResponseMessage>
```

---

### PatchAsync()
- Used to partially update a resource.

**HTTP Method:** PATCH


**Example:**
```cs
await client.PatchAsync("api/employees/1", content);
```

**Use Cases:**
- Update Salary Only
- Update Status Only

**Return Type:**
```cs
Task<HttpResponseMessage>
```

---

### DeleteAsync()
- Used to delete a resource.

**HTTP Method:** DELETE

**Example:**
```cs
await client.DeleteAsync("api/employees/1");
```

**Use Cases:**
- Delete Employee
- Delete Product

**Return Type:**
```cs
Task<HttpResponseMessage>
```

---

### SendAsync()
- Most flexible method.
- Used when custom request configuration is needed.

**Example:**
```cs
HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, "api/employees");
HttpResponseMessage response = await client.SendAsync(request);
```

**Supports:**
- GET
- POST
- PUT
- PATCH
- DELETE
- HEAD
- OPTIONS

**Return Type:**
```cs
Task<HttpResponseMessage>
```

---

### GetStringAsync()
- Downloads response directly as string.

**Example:**
```cs
string result = await client.GetStringAsync("api/employees");
```

**Output:**
- JSON
- HTML
- XML
- Plain Text

**Return Type:**
```cs
Task<string>
```

---

### GetByteArrayAsync()
- Downloads response as byte array.

**Example:**
```cs
byte[] data = await client.GetByteArrayAsync("image.jpg");
```

**Used For:**
- Images
- PDF Files
- Binary Data
- Documents

Return Type:
```cs
Task<byte[]>
```

---

### GetStreamAsync()
- Downloads response as stream.

**Example:**
```cs
Stream stream = await client.GetStreamAsync("video.mp4");
```

**Used For:**
- Large Files
- Video Streaming
- Audio Streaming
- File Downloads

**Return Type:**
```cs
Task<Stream>
```

---








# HttpMethod.Get

## Purpose

Retrieve data from server.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Get,
        "employees");
```

or

```cs
await client.GetAsync(
    "employees");
```

Used For:

```text
Get Employees

Get Products

Get Orders
```

---

# HttpMethod.Post

## Purpose

Create new data.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Post,
        "employees");
```

or

```cs
await client.PostAsync(
    "employees",
    content);
```

Used For:

```text
Add Employee

Create Product

Register User
```

---

# HttpMethod.Put

## Purpose

Update entire resource.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Put,
        "employees/1");
```

or

```cs
await client.PutAsync(
    "employees/1",
    content);
```

Used For:

```text
Update Employee

Update Product
```

---

# HttpMethod.Patch

## Purpose

Update partial resource.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Patch,
        "employees/1");
```

Used For:

```text
Update Salary Only

Update Email Only
```

---

# HttpMethod.Delete

## Purpose

Delete resource.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Delete,
        "employees/1");
```

or

```cs
await client.DeleteAsync(
    "employees/1");
```

Used For:

```text
Delete Employee

Delete Product
```

---

# HttpMethod.Head

## Purpose

Get headers only.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Head,
        "employees");
```

Used For:

```text
Check Resource Exists

Get Header Information
```

---

# HttpMethod.Options

## Purpose

Get supported methods.

Example:

```cs
var request =
    new HttpRequestMessage(
        HttpMethod.Options,
        "employees");
```

Used For:

```text
Check Allowed Methods

CORS Requests
```