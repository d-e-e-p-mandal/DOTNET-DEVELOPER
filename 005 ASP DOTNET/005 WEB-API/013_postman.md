# 2. Postman

---

# What is Postman?

Postman is API testing software.

Used to:
- Send HTTP requests
- Test APIs
- Verify responses

---

# Postman Features

- API testing
- Header management
- JWT testing
- File upload testing
- Environment variables
- Collection management

---

# Common HTTP Methods

| Method | Purpose |
|---|---|
| GET | Read data |
| POST | Create data |
| PUT | Update data |
| DELETE | Delete data |
| PATCH | Partial update |

---

# Example API

```cs
[HttpGet]
public IActionResult Get()
{
    return Ok("Employee List");
}
```

---

# Testing GET API in Postman

## Method

```text
GET
```

---

# URL

```text
https://localhost:5001/api/employee
```

---

# Click

```text
Send
```

---

# Response

```json
"Employee List"
```

---

# Testing POST API

---

# API Example

```cs
[HttpPost]
public IActionResult Create(Employee employee)
{
    return Ok(employee);
}
```

---

# Request Body

```json
{
  "id": 1,
  "name": "Deep"
}
```

---

# Postman Setup

## Method

```text
POST
```

---

# Body Type

```text
raw → JSON
```

---

# Response

```json
{
  "id": 1,
  "name": "Deep"
}
```

---

# Postman Request Flow

```text
Postman Sends Request
         ↓
API Receives Request
         ↓
Controller Executes
         ↓
Response Returned
         ↓
Postman Displays Response
```

---

# Headers in Postman

Headers contain extra request information.

---

# Common Headers

| Header | Purpose |
|---|---|
| Content-Type | Data type |
| Authorization | JWT token |
| Accept | Response type |

---

# Example Header

```text
Content-Type: application/json
```

---

# JWT Authentication in Postman

---

# Authorization Header

```text
Authorization: Bearer TOKEN
```

---

# Purpose

Used to access secured APIs.

---

# Postman File Upload

---

# Method

```text
POST
```

---

# Body Type

```text
form-data
```

---

# Key Type

```text
File
```

---

# Purpose

Test File Upload APIs.

---

# Postman Collections

---

# What is Collection?

Group of saved APIs.

---

# Benefits

- Reuse requests
- Organize APIs
- Team sharing

---

# Environment Variables

---

# Purpose

Store:
- Base URL
- Tokens
- API keys

---

# Example

```text
{{baseUrl}}/api/employee
```

---

# Postman Advantages

- Powerful testing
- Advanced features
- JWT support
- File upload support
- Environment support

---

# Postman Disadvantages

- Separate software needed
- Manual setup required

---