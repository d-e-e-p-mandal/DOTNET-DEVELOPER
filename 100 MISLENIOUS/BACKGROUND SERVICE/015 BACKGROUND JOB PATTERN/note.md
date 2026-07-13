# 15. Background Job Patterns

A summary of the major architectural patterns used when designing background work, and when to reach for each.

## Fire-And-Forget Jobs

The simplest pattern: trigger a job and don't wait for or track its result.

```csharp
[HttpPost("notify")]
public IActionResult Notify()
{
    _ = Task.Run(() => SendNotificationAsync()); // fire-and-forget — risky, see caveats
    return Accepted();
}
```

**Caveats:**
- Exceptions are unobserved unless explicitly caught inside the fired task.
- No retry, no persistence — if the process restarts mid-flight, the work is lost.
- Generally discouraged for anything important; prefer the Queue-Based pattern below even for "simple" fire-and-forget needs, so failures are visible and retryable.

**Better approach using a hosted queue (safe fire-and-forget):**
```csharp
await _backgroundTaskQueue.QueueAsync(async token => await SendNotificationAsync(token));
```
This still "fires and forgets" from the caller's perspective, but a dedicated consumer (a `BackgroundService`) owns execution, logging, and error handling.

## Scheduled Jobs

Work that runs at specific times, regardless of any external trigger — "every day at 2 AM," "every 15 minutes."

```csharp
// Simple anchored scheduling inside a BackgroundService (see Timers section for full pattern)
var nextRun = ComputeNextRunTime();
await Task.Delay(nextRun - DateTime.Now, stoppingToken);
await RunScheduledJobAsync(stoppingToken);
```

For non-trivial schedules (multiple jobs, cron expressions, persistence across restarts), use **Quartz.NET** or **Hangfire**:

```csharp
// Quartz.NET
q.AddTrigger(opts => opts.ForJob("cleanupJob").WithCronSchedule("0 0 3 * * ?"));

// Hangfire
RecurringJob.AddOrUpdate("cleanup-job", () => CleanupService.Run(), Cron.Daily);
```

## Recurring Jobs

A subtype of scheduled jobs that repeat indefinitely on a fixed cadence (as opposed to a one-time future-scheduled job). The `PeriodicTimer`/`Task.Delay` loop pattern inside `ExecuteAsync` IS a recurring job mechanism by nature. Hangfire/Quartz formalize this with named recurring job definitions that survive restarts and are visible/manageable via a dashboard or API.

## Queue-Based Jobs

Work items are placed on a queue (in-memory `Channel<T>`, or a durable broker like RabbitMQ/Azure Service Bus) and a `BackgroundService` consumer drains them — covered in depth in the Queues section. This is the preferred pattern when:
- Work arrives unpredictably (not on a schedule).
- You want to decouple "who creates the work" from "who processes it."
- You may need to scale out multiple consumers for throughput.

```csharp
public class QueuedHostedService : BackgroundService
{
    private readonly IBackgroundTaskQueue _taskQueue;

    public QueuedHostedService(IBackgroundTaskQueue taskQueue) => _taskQueue = taskQueue;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            var workItem = await _taskQueue.DequeueAsync(stoppingToken);
            try { await workItem(stoppingToken); }
            catch (Exception ex) { /* log */ }
        }
    }
}
```

## Event-Driven Jobs

Work is triggered by an external **event** rather than a poll/schedule — e.g., a file-system watcher event, a message arriving on a broker, a domain event published inside the app (via something like `MediatR` or an in-process event bus), or a webhook callback hitting an API endpoint that then enqueues work.

```csharp
// FileSystemWatcher example — reacts to file creation events rather than polling
public class FileWatcherService : BackgroundService
{
    private readonly string _watchPath;
    private readonly Channel<string> _channel;

    protected override Task ExecuteAsync(CancellationToken stoppingToken)
    {
        var watcher = new FileSystemWatcher(_watchPath)
        {
            EnableRaisingEvents = true,
            NotifyFilter = NotifyFilters.FileName
        };

        watcher.Created += async (s, e) => await _channel.Writer.WriteAsync(e.FullPath, stoppingToken);

        stoppingToken.Register(() => watcher.Dispose());
        return Task.CompletedTask;
    }
}
```

The "trigger" (file created, message published) is fundamentally different from a timer/poll: the service reacts immediately rather than discovering work on its next scheduled check, which reduces latency and avoids wasted polling cycles.

---

## Choosing the Right Pattern

| Scenario | Best Pattern |
|---|---|
| "Send this one email, don't make the user wait" | Queue-based (safe fire-and-forget via a hosted queue) |
| "Run a report every night at 2 AM" | Scheduled / Recurring (Quartz.NET, Hangfire, or anchored `Task.Delay`) |
| "Process orders as they come in, from many producers" | Queue-based (in-memory `Channel<T>` or external broker) |
| "React the instant a file lands in a folder" | Event-driven (`FileSystemWatcher` + queue) |
| "Process must survive app restarts and be retryable with a dashboard" | Hangfire (persisted jobs) or a durable broker (RabbitMQ/Azure Service Bus) |
| "Need precise cron-style scheduling with multiple jobs" | Quartz.NET |

## Combining Patterns
Real systems often combine several: e.g., a **scheduled job** (runs nightly) that **enqueues** a batch of **queue-based jobs** (one per record to process), consumed by a pool of worker `BackgroundService` instances, with **event-driven** triggers (webhook) able to enqueue additional ad-hoc work outside the nightly schedule.