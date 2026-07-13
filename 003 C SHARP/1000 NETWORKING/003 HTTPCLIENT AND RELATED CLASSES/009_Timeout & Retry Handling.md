
# Timeout & Retry Handling

## What is Timeout?
- A **Timeout** is the **maximum amount of time** that `HttpClient` waits for a server response.

## What is Retry Handling?
**Retry Handling** is the process of **automatically sending the same HTTP request again** when a temporary failure occurs.
Retry is useful for failures such as:
- Temporary network issues
- Server temporarily unavailable
- Request timeout


**Timeout Flow:**
```text
Application
      │
      ▼
Send HTTP Request
      │
      ▼
Wait for Response
      │
      ├──────────────► Response received within timeout
      │                     │
      │                     ▼
      │                 Success
      │
      └──────────────► Timeout reached
                            │
                            ▼
                    Request Cancelled
```

**Retry Flow:**
```text
Request
   │
   ▼
Failed
   │
   ▼
Retry #1
   │
   ▼
Failed
   │
   ▼
Retry #2
   │
   ▼
Success
```

### Default Timeout : 100 s 
- 100 s (1:40)

### Set Timeout : Custom
- Use the `Timeout` property of `HttpClient`.

```csharp
HttpClient client = new HttpClient();

client.Timeout = TimeSpan.FromSeconds(30);
```


## Time Out Exception : TaskCanceledException

```csharp
HttpClient client = new HttpClient();
client.Timeout = TimeSpan.FromSeconds(10);

try
{
    string data = await client.GetStringAsync("https://example.com/api/users");
}
catch (TaskCanceledException)
{
    Console.WriteLine("Request timed out.");
}
```


**What Happens When Timeout Occurs?**
```text
Request Sent
      │
      ▼
Server is Slow
      │
      ▼
Timeout Reached
      │
      ▼
TaskCanceledException
```


## Retry Example: Manual
- Retry logic can be written using a loop.

```csharp
HttpClient client = new HttpClient();

int maxRetries = 3;

for (int attempt = 1; attempt <= maxRetries; attempt++)
{
    try
    {
        string data = await client.GetStringAsync("https://example.com/api/users");

        Console.WriteLine(data);

        break;
    }
    catch
    {
        Console.WriteLine($"Attempt {attempt} failed.");

        if (attempt == maxRetries)
        {
            Console.WriteLine("Maximum retry limit reached.");
        }
    }
}
```


## Retry with Delay
- Sometimes it is better to wait before retrying.

```csharp
HttpClient client = new HttpClient();

int maxRetries = 3;

for (int attempt = 1; attempt <= maxRetries; attempt++)
{
    try
    {
        string data = await client.GetStringAsync("https://example.com/api/users");

        Console.WriteLine(data);

        break;
    }
    catch
    {
        Console.WriteLine($"Retry {attempt}");

        await Task.Delay(2000);
    }
}
```

The application waits **2 seconds** before each retry.

---

### When Should You Retry?

Retry only for **temporary failures**.

Examples:

- Timeout
- Network interruption
- HTTP 500
- HTTP 502
- HTTP 503
- HTTP 504


### When Should You NOT Retry?
Do **not** retry when the request is invalid.

Examples:

- HTTP 400 Bad Request
- HTTP 401 Unauthorized
- HTTP 403 Forbidden
- HTTP 404 Not Found

Retrying these requests usually produces the same result.

---

# Timeout vs Retry

| Timeout | Retry |
|---------|-------|
| Limits waiting time | Sends the request again |
| Prevents long waits | Handles temporary failures |
| Stops a slow request | Attempts recovery |
| Uses `Timeout` property | Uses retry logic |

---

## Advantages

### Timeout

- Prevents applications from hanging.
- Improves responsiveness.
- Frees system resources.

### Retry Handling

- Improves reliability.
- Handles temporary failures.
- Increases the chance of a successful request.


## Limitations

### Timeout

- A timeout that is too short may cancel valid requests.
- A timeout that is too long may make the application feel slow.

### Retry Handling

- Too many retries increase server load.
- Retrying permanent failures is unnecessary.
- Delays caused by retries can increase total response time.

---

# Best Practices

- Always set a reasonable timeout.
- Retry only for temporary failures.
- Limit the number of retry attempts.
- Add a delay between retries.
- Do not retry client errors such as **400**, **401**, **403**, or **404**.
- In ASP.NET Core, use resilience libraries (for example, Polly integration with `IHttpClientFactory`) for advanced retry policies instead of writing retry loops manually.

---

# Interview Questions

### 1. What is Timeout?

Timeout is the maximum amount of time that `HttpClient` waits for a server response.

---

### 2. What happens when a timeout occurs?

The request is cancelled, and a `TaskCanceledException` is typically thrown.

---

### 3. What is Retry Handling?

Retry Handling is the process of automatically sending a failed request again when the failure is temporary.

---

### 4. Should every failed request be retried?

No. Only temporary failures should be retried. Permanent errors such as **400 Bad Request** or **404 Not Found** should not.

---

### 5. Why should there be a delay between retries?

A delay gives the server or network time to recover and helps avoid sending repeated requests too quickly.

---