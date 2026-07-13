# 14. Queues

In-process queues let one part of your application (a "producer") hand off work to another part (a "consumer" — typically a `BackgroundService`) without them needing to call each other directly or block on completion.

## In-Memory Queue Options

### `ConcurrentQueue<T>`
A thread-safe FIFO collection — multiple threads can enqueue/dequeue concurrently without manual locking.

```csharp
private readonly ConcurrentQueue<string> _queue = new();

// Producer
_queue.Enqueue("job-123");

// Consumer
if (_queue.TryDequeue(out var job))
{
    Process(job);
}
```

⚠️ Limitation: `ConcurrentQueue` has **no built-in blocking/waiting mechanism** — a consumer must poll (`TryDequeue` in a loop with a delay) rather than asynchronously wait for an item to arrive. This wastes CPU on empty polling and adds latency.

### `BlockingCollection<T>`
Wraps a thread-safe collection (commonly a `ConcurrentQueue<T>` internally) and adds **blocking** add/take semantics — a consumer thread can block until an item becomes available.

```csharp
private readonly BlockingCollection<string> _queue = new();

// Producer
_queue.Add("job-123");

// Consumer (blocks the calling thread until an item is available)
foreach (var job in _queue.GetConsumingEnumerable(stoppingToken))
{
    Process(job);
}

// When done producing:
_queue.CompleteAdding();
```

⚠️ Limitation: `BlockingCollection` is **synchronous** — it blocks the actual thread while waiting, not `async`-friendly. Using it inside an `async ExecuteAsync` loop risks tying up a thread-pool thread unnecessarily.

### `Channel<T>` (Modern, Recommended for Async Producer/Consumer)
Part of `System.Threading.Channels` — a fully `async`-native, thread-safe queue designed exactly for the producer/consumer pattern, with optional bounded capacity and back-pressure handling.

```csharp
var channel = Channel.CreateUnbounded<string>();

// Producer
await channel.Writer.WriteAsync("job-123");

// Consumer
while (await channel.Reader.WaitToReadAsync(stoppingToken))
{
    while (channel.Reader.TryRead(out var job))
    {
        await ProcessAsync(job, stoppingToken);
    }
}
```

#### Bounded Channels (Back-Pressure)
```csharp
var channel = Channel.CreateBounded<string>(new BoundedChannelOptions(capacity: 100)
{
    FullMode = BoundedChannelFullMode.Wait // producers wait if the queue is full
});
```

`BoundedChannelFullMode` options:
- `Wait` — producer awaits until space is available (back-pressure — prevents unbounded memory growth).
- `DropOldest` / `DropNewest` — discard items instead of blocking the producer.
- `DropWrite` — the newly written item itself is dropped if full.

`Channel<T>` is the **modern standard choice** for in-memory background task queues in .NET — it's what underlies many "queued background task" implementations seen in official samples.

---

## Producer-Consumer Pattern

The general architecture:

```
┌────────────┐   enqueue   ┌─────────────┐   dequeue   ┌──────────────┐
│  Producer   │ ──────────▶ │    Queue     │ ──────────▶ │  Consumer     │
│ (API request,│             │ (Channel<T>, │             │ (BackgroundService│
│  event, etc.)│             │ ConcurrentQ) │             │  ExecuteAsync)   │
└────────────┘             └─────────────┘             └──────────────┘
```

### Producer
Anything that creates work — an API controller receiving a request, an event handler, another background service.

```csharp
public class JobsController : ControllerBase
{
    private readonly Channel<EmailJob> _channel;

    public JobsController(Channel<EmailJob> channel) => _channel = channel;

    [HttpPost("send-email")]
    public async Task<IActionResult> SendEmail(EmailJob job)
    {
        await _channel.Writer.WriteAsync(job);
        return Accepted();
    }
}
```

### Consumer
A `BackgroundService` that continuously reads from the queue and processes items.

```csharp
public class EmailQueueConsumer : BackgroundService
{
    private readonly Channel<EmailJob> _channel;
    private readonly IServiceScopeFactory _scopeFactory;

    public EmailQueueConsumer(Channel<EmailJob> channel, IServiceScopeFactory scopeFactory)
    {
        _channel = channel;
        _scopeFactory = scopeFactory;
    }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (await _channel.Reader.WaitToReadAsync(stoppingToken))
        {
            while (_channel.Reader.TryRead(out var job))
            {
                using var scope = _scopeFactory.CreateScope();
                var emailService = scope.ServiceProvider.GetRequiredService<IEmailService>();
                await emailService.SendAsync(job, stoppingToken);
            }
        }
    }
}
```

### Queue Processing — Design Considerations
1. **Bounded vs unbounded**: bounded queues protect against memory blow-up if producers outpace consumers; unbounded risk unbounded memory growth under sustained overload.
2. **Single vs multiple consumers**: you can run multiple consumer loops (e.g., `Parallel.ForEachAsync` over the channel reader, or multiple `BackgroundService` instances) to increase throughput, but then you must handle ordering/concurrency implications.
3. **Durability**: in-memory queues (`Channel<T>`, `ConcurrentQueue`) **lose all queued items if the process crashes or restarts** — fine for non-critical, retryable work; NOT fine for things like financial transactions, where a real message broker (RabbitMQ, Azure Service Bus, Kafka — see Messaging Systems) or a database-backed queue table is required.
4. **Back-pressure**: if consumers can't keep up, bounded channels (or external queue depth limits) prevent the producer side from overwhelming memory/resources.
5. **Idempotency**: consumers should handle being given the same item twice gracefully (e.g., after a crash-and-retry), especially once you move beyond pure in-memory queues to anything with at-least-once delivery semantics.

### Registering a Shared `Channel<T>` in DI
```csharp
builder.Services.AddSingleton(Channel.CreateUnbounded<EmailJob>());
builder.Services.AddHostedService<EmailQueueConsumer>();
```

Registering the `Channel<T>` itself as a Singleton means both the API controller (producer) and the background service (consumer) can inject the *same* channel instance and communicate through it safely across the whole app.