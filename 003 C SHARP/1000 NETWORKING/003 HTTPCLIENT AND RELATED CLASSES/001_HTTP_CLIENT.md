# HttpClient in .NET
- `HttpClient` is a class in .NET that is used to send HTTP requests to a web server and receive HTTP responses.

It is commonly used to:
- Call REST APIs
- Send data to a server
- Receive data from a server
- Communicate with web services


### Namespace

```csharp
using System.Net.Http;
```

**Create an HttpClient:**
```csharp
HttpClient client = new HttpClient();
```
- The `HttpClient` object is responsible for sending HTTP requests.


### HTTP Methods

| HTTP Method | Purpose |
|-------------|----------|
| GET | Read data from the server |
| POST | Create new data |
| PUT | Update existing data |
| PATCH | Update part of existing data |
| DELETE | Delete data |


----------


## HTTP-Handler: Class Hierarchy

```text
HttpMessageHandler (Abstract)
        ▲
        │
 ┌──────┴──────────────┐
 │                     │
 ▼                     ▼
HttpClientHandler   DelegatingHandler
                           ▲
                           │
                    Custom Handler
```


--------
--------

### GET Request (Method 1 - Simple)

- This is the easiest way to perform a GET request.
- Use `GetStringAsync()` when you only need the response data.

```csharp
HttpClient client = new HttpClient();

string data = await client.GetStringAsync(
    "https://jsonplaceholder.typicode.com/posts/1");

Console.WriteLine(data);
```

### Output

```json
{
    "userId":1,
    "id":1,
    "title":"Sample Title",
    "body":"Sample Body"
}
```

### Flow
```
Client
   │
   │ GET Request
   ▼
Server
   │
   │ JSON Response
   ▼
string data
```

### When to use

- Simple API calls
- Reading JSON
- Beginners

---

# GET Request (Method 2 - Advanced)

- Sometimes you need more than the response body then Use `GetAsync()`.

```csharp
HttpClient client = new HttpClient();

HttpResponseMessage response =
    await client.GetAsync("https://jsonplaceholder.typicode.com/posts/1");
```
- This returns a `HttpResponseMessage` object.


# What is HttpResponseMessage?

`HttpResponseMessage` stores the complete response received from the server.

It contains:

- Status Code
- Headers
- Content
- Success information

```
HttpResponseMessage
│
├── StatusCode
├── Headers
├── Content
└── IsSuccessStatusCode
```

---

## Read Response Body

The response object contains many things.

The actual JSON data is stored inside `Content`.

```csharp
string data = await response.Content.ReadAsStringAsync();

Console.WriteLine(data);
```

### Flow

```
response
     │
     ▼
Content
     │
     ▼
ReadAsStringAsync()
     │
     ▼
JSON String
```

## Check Status Code

Always check whether the request was successful.

```csharp
if (response.IsSuccessStatusCode)
{
    Console.WriteLine("Request Successful");
}
else
{
    Console.WriteLine("Request Failed");
}
```


### Complete GET Example

```csharp
using System;
using System.Net.Http;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        HttpClient client = new HttpClient();

        HttpResponseMessage response =
            await client.GetAsync("https://jsonplaceholder.typicode.com/posts/1");

        if (response.IsSuccessStatusCode)
        {
            string data = await response.Content.ReadAsStringAsync();

            Console.WriteLine(data);
        }
    }
}
```

---

# POST Request

- POST sends new data to the server.

```csharp
using System.Text;

HttpClient client = new HttpClient();

string json =
@"{
    ""name"":""John"",
    ""age"":25
}";

StringContent content = new StringContent(json,
                                        Encoding.UTF8,
                                        "application/json");

HttpResponseMessage response =
    await client.PostAsync("https://example.com/api/users", content);
```

---

## PUT Request

PUT updates an existing resource.

```csharp
using System.Text;

string json =
@"{
    ""name"":""Alice""
}";

StringContent content = new StringContent(json,
                                    Encoding.UTF8,
                                    "application/json");

HttpResponseMessage response = await client.PutAsync("https://example.com/api/users/1", content);
```

----

## PATCH Request

- PATCH updates only part of an existing resource.

```csharp
using System.Text;

string json =
@"{
    ""name"":""Bob""
}";

StringContent content = new StringContent(
                                json,
                                Encoding.UTF8,
                                "application/json");

HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Patch, "https://example.com/api/users/1");

request.Content = content;

HttpResponseMessage response = await client.SendAsync(request);
```

---

## DELETE Request

DELETE removes data from the server.

```csharp
HttpClient client = new HttpClient();

HttpResponseMessage response = await client.DeleteAsync("https://example.com/api/users/1");
```

---

## Set Base Address

Instead of writing the full URL every time:

```csharp
HttpClient client = new HttpClient();

client.BaseAddress = new Uri("https://example.com/");
```

**Now simply write:**
```csharp
await client.GetAsync("api/users");
```

**instead of**
```csharp
await client.GetAsync("https://example.com/api/users");
```

---

# Add Headers

```csharp
client.DefaultRequestHeaders.Add(
    "User-Agent",
    "MyApplication");
```

---

# Authorization Header

```csharp
using System.Net.Http.Headers;

client.DefaultRequestHeaders.Authorization =
    new AuthenticationHeaderValue(
        "Bearer",
        "your_token_here");
```

---

# Timeout

```csharp
client.Timeout =
    TimeSpan.FromSeconds(30);
```

If the server does not respond within 30 seconds, the request fails.

---

# Read JSON Directly

Instead of reading a string manually, .NET can convert JSON into an object.

```csharp
using System.Net.Http.Json;

User user =
    await client.GetFromJsonAsync<User>(
        "https://example.com/api/users/1");
```

Model

```csharp
public class User
{
    public int Id { get; set; }

    public string Name { get; set; }
}
```

---

# Send Object as JSON

```csharp
using System.Net.Http.Json;

User user = new User
{
    Name = "John"
};

await client.PostAsJsonAsync("https://example.com/api/users", user);
```

---

# Exception Handling

```csharp
try
{
    HttpClient client = new HttpClient();

    string data =
        await client.GetStringAsync(
            "https://example.com");
}
catch (Exception ex)
{
    Console.WriteLine(ex.Message);
}
```

---

# GetStringAsync() vs GetAsync()

| GetStringAsync() | GetAsync() |
|------------------|------------|
| Returns only response body | Returns complete HTTP response |
| Easy to use | More powerful |
| No status code | Status code available |
| No headers | Headers available |
| Best for beginners | Best for real-world applications |

---

# Best Practices

- Reuse the same `HttpClient` instance.
- Always use `async` and `await`.
- Check `IsSuccessStatusCode`.
- Set a timeout.
- Handle exceptions.
- Use `GetStringAsync()` for simple GET requests.
- Use `GetAsync()` when you need status code or headers.
- Use `IHttpClientFactory` in ASP.NET Core applications.

---

# Advantages

- Simple to use
- Supports asynchronous programming
- Supports REST APIs
- Supports JSON, XML, and text
- Supports authentication
- Supports custom headers
- Supports timeout configuration