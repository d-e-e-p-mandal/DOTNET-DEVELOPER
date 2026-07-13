# 18. Networking in Background Services

## `HttpClient`

The standard class for making HTTP calls. In background services, used for polling external APIs, calling webhooks, pushing data to other systems, etc.

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        var response = await _httpClient.GetAsync("https://api.example.com/status", stoppingToken);
        response.EnsureSuccessStatusCode();
        var body = await response.Content.ReadAsStringAsync(stoppingToken);
        await Task.Delay(TimeSpan.FromSeconds(30), stoppingToken);
    }
}
```

⚠️ **Never `new HttpClient()` repeatedly** inside a loop — each instance opens its own connection pool, and frequent creation/disposal can exhaust OS sockets (especially under DNS changes) or leak handles. This is exactly why `IHttpClientFactory` exists.

## `IHttpClientFactory`

The recommended way to obtain `HttpClient` instances — manages the underlying `HttpMessageHandler` pool correctly (handling DNS refresh, connection reuse, and avoiding socket exhaustion).

### Basic Registration
```csharp
builder.Services.AddHttpClient(); // registers IHttpClientFactory

public class ApiPollerWorker : BackgroundService
{
    private readonly IHttpClientFactory _httpClientFactory;

    public ApiPollerWorker(IHttpClientFactory httpClientFactory) => _httpClientFactory = httpClientFactory;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        var client = _httpClientFactory.CreateClient();
        while (!stoppingToken.IsCancellationRequested)
        {
            var data = await client.GetStringAsync("https://api.example.com/data", stoppingToken);
            await Task.Delay(TimeSpan.FromMinutes(1), stoppingToken);
        }
    }
}
```

### Named/Typed Clients (Preferred for Multiple External APIs)
```csharp
builder.Services.AddHttpClient("PaymentGateway", client =>
{
    client.BaseAddress = new Uri("https://payments.example.com/");
    client.Timeout = TimeSpan.FromSeconds(15);
});

// usage:
var client = _httpClientFactory.CreateClient("PaymentGateway");
```

```csharp
// Typed client — strongly typed wrapper class injected directly
public class PaymentApiClient
{
    private readonly HttpClient _httpClient;
    public PaymentApiClient(HttpClient httpClient) => _httpClient = httpClient;

    public Task<PaymentStatus> GetStatusAsync(string id, CancellationToken token) =>
        _httpClient.GetFromJsonAsync<PaymentStatus>($"status/{id}", token);
}

builder.Services.AddHttpClient<PaymentApiClient>(client =>
{
    client.BaseAddress = new Uri("https://payments.example.com/");
});
```

## API Polling

Periodically calling an external API to check for new data/status changes — common when the external system doesn't support webhooks/push notifications.

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    using var timer = new PeriodicTimer(TimeSpan.FromSeconds(60));
    while (await timer.WaitForNextTickAsync(stoppingToken))
    {
        var client = _httpClientFactory.CreateClient("ExternalApi");
        var updates = await client.GetFromJsonAsync<List<Update>>("updates/since?lastId=" + _lastId, stoppingToken);
        foreach (var update in updates ?? Enumerable.Empty<Update>())
        {
            await ProcessUpdateAsync(update, stoppingToken);
            _lastId = update.Id;
        }
    }
}
```

## Webhook Processing

Webhooks invert the polling model — the external system pushes data to **your** API endpoint when something happens. The endpoint itself usually does minimal work (validate signature, enqueue the payload) and a `BackgroundService` consumer processes it asynchronously, keeping the webhook response fast (most providers expect a quick 200 OK or they'll retry/back off).

```csharp
[HttpPost("webhooks/payment")]
public async Task<IActionResult> PaymentWebhook([FromBody] PaymentEvent evt)
{
    if (!IsValidSignature(Request)) return Unauthorized();
    await _taskQueue.QueueAsync(token => ProcessPaymentEventAsync(evt, token));
    return Ok(); // respond fast; actual processing happens in the background
}
```

## REST APIs vs SOAP APIs

| | REST | SOAP |
|---|---|---|
| Format | Typically JSON over HTTP | XML envelope (WS-* standards) |
| .NET tooling | `HttpClient` + `System.Text.Json` | `HttpClient` + manual XML, or generated client via WCF Connected Service / `dotnet-svcutil` |
| Common in | Modern APIs, most third-party services | Legacy enterprise systems, some banking/government integrations |

Background services integrating with **older banking/enterprise partners** (common in NACH/ACH-adjacent systems) sometimes still need to call SOAP endpoints — typically handled by generating a client proxy from the WSDL and wrapping calls with the same retry/timeout/logging discipline as any REST call.

```csharp
// SOAP-ish manual call via HttpClient (when no generated client is available)
var soapEnvelope = BuildSoapEnvelope(request);
var content = new StringContent(soapEnvelope, Encoding.UTF8, "text/xml");
content.Headers.Add("SOAPAction", "\"http://example.com/GetStatus\"");
var response = await client.PostAsync(soapUrl, content, stoppingToken);
```

---

## HttpClient Concepts

### Timeout
```csharp
client.Timeout = TimeSpan.FromSeconds(30); // overall request timeout
```
Or per-request, using a linked `CancellationTokenSource`:
```csharp
using var cts = CancellationTokenSource.CreateLinkedTokenSource(stoppingToken);
cts.CancelAfter(TimeSpan.FromSeconds(10));
var response = await client.GetAsync(url, cts.Token);
```

### Retry
Handled at the application level — typically via **Polly** (see Resilience Patterns section) combined with `IHttpClientFactory`'s `AddPolicyHandler`:
```csharp
builder.Services.AddHttpClient("ExternalApi")
    .AddPolicyHandler(Policy<HttpResponseMessage>
        .Handle<HttpRequestException>()
        .OrResult(r => !r.IsSuccessStatusCode)
        .WaitAndRetryAsync(3, attempt => TimeSpan.FromSeconds(Math.Pow(2, attempt))));
```

### Headers
```csharp
client.DefaultRequestHeaders.Add("X-Api-Version", "2.0");
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);
```

### Authentication
Common patterns: static API key headers, OAuth2 client-credentials tokens (often cached and refreshed by a `DelegatingHandler`), mutual TLS certificates for high-security banking integrations.

### `DelegatingHandler`
A pluggable middleware-style component you can chain into an `HttpClient` pipeline — useful for cross-cutting concerns like automatically attaching auth tokens, logging every request/response, or injecting correlation IDs.

```csharp
public class AuthHeaderHandler : DelegatingHandler
{
    private readonly ITokenProvider _tokenProvider;
    public AuthHeaderHandler(ITokenProvider tokenProvider) => _tokenProvider = tokenProvider;

    protected override async Task<HttpResponseMessage> SendAsync(
        HttpRequestMessage request, CancellationToken cancellationToken)
    {
        var token = await _tokenProvider.GetTokenAsync(cancellationToken);
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", token);
        return await base.SendAsync(request, cancellationToken);
    }
}

builder.Services.AddTransient<AuthHeaderHandler>();
builder.Services.AddHttpClient("SecureApi")
    .AddHttpMessageHandler<AuthHeaderHandler>();
```

This keeps your background service's polling/processing logic clean — auth, logging, and retry concerns live in the handler pipeline, not scattered throughout business logic.