# 12. Cancellation

## `CancellationToken`

A lightweight, immutable struct passed through async call chains to signal that an operation should be cancelled. It doesn't *force* cancellation — cooperating code must check it (or pass it to APIs that check it internally, like `Task.Delay`, `HttpClient`, EF Core methods).

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        await DoWorkAsync(stoppingToken);
        await Task.Delay(5000, stoppingToken);
    }
}
```

## `CancellationTokenSource`

The object that actually *produces* and *controls* a `CancellationToken`. You create one, hand out its `.Token` to consumers, and call `.Cancel()` on the source when you want to signal cancellation.

```csharp
var cts = new CancellationTokenSource();
CancellationToken token = cts.Token;

// elsewhere:
cts.Cancel(); // triggers cancellation for anyone holding `token`
```

You can also create a source with an automatic timeout:
```csharp
using var cts = new CancellationTokenSource(TimeSpan.FromSeconds(30));
await SomeOperationAsync(cts.Token); // auto-cancels after 30s
```

Or **link** multiple tokens together (cancel if EITHER source cancels):
```csharp
using var linkedCts = CancellationTokenSource.CreateLinkedTokenSource(stoppingToken, timeoutCts.Token);
await DoWorkAsync(linkedCts.Token);
```
This pattern is very useful in background services: combine the host's `stoppingToken` (app shutting down) with a per-operation timeout token (this single job took too long), so either condition cancels the work.

## `Cancel()`
Signals all consumers of tokens derived from this source that cancellation has been requested. This doesn't immediately stop anything by itself — it sets `IsCancellationRequested = true` and triggers any registered callbacks; cooperating code is responsible for actually halting.

## `ThrowIfCancellationRequested()`

```csharp
foreach (var item in items)
{
    stoppingToken.ThrowIfCancellationRequested(); // throws OperationCanceledException if cancelled
    Process(item);
}
```

A convenient guard you sprinkle inside loops/long sequences of synchronous work, so cancellation is honored even if there's no natural `await` point to pass the token to.

## `IsCancellationRequested`

A boolean property you can check without throwing — useful for loop conditions where you want to exit gracefully rather than via exception.

```csharp
while (!stoppingToken.IsCancellationRequested)
{
    // ...
}
```

---

## Background Service Cancellation — How It All Connects

When `BackgroundService.StopAsync` is called by the host (during shutdown), the base class internally calls `Cancel()` on the `CancellationTokenSource` whose `.Token` was passed into your `ExecuteAsync` as `stoppingToken`. That's the entire mechanism:

```
Host shutdown begins
        │
        ▼
BackgroundService.StopAsync() called
        │
        ▼
internal _stoppingCts.Cancel()
        │
        ▼
stoppingToken.IsCancellationRequested = true
        │
        ▼
Any in-flight await Task.Delay(..., stoppingToken) immediately throws OperationCanceledException
        │
        ▼
Your while loop's condition check (or the exception) ends the loop
        │
        ▼
ExecuteAsync's Task completes
        │
        ▼
StopAsync finishes awaiting that task (or times out per HostOptions.ShutdownTimeout)
```

## Shutdown Handling — Practical Pattern

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    _logger.LogInformation("Worker starting.");

    try
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            await DoUnitOfWorkAsync(stoppingToken);
            await Task.Delay(TimeSpan.FromSeconds(15), stoppingToken);
        }
    }
    catch (OperationCanceledException)
    {
        // This is the EXPECTED, normal way the loop ends during shutdown — not an error.
        _logger.LogInformation("Worker cancellation requested — shutting down gracefully.");
    }
    finally
    {
        _logger.LogInformation("Worker stopped.");
    }
}
```

## Graceful Stop — Why It Matters

"Graceful" means: when asked to stop, the service finishes (or safely aborts) whatever it's currently doing, releases resources properly (closes connections, flushes buffers, commits/rolls back transactions), and exits within the shutdown timeout — rather than being abruptly killed mid-operation, which can leave data half-written, files half-processed, or external resources (locks, connections) leaked.

### Key Practices for Graceful Stop
1. **Always pass `stoppingToken`** into every awaitable call inside the loop (`Task.Delay`, DB calls, HTTP calls, queue reads).
2. **Check cancellation between logical units of work**, not just at the top of a `while` loop, especially if a single iteration processes a large batch.
3. **Keep individual units of work short** where possible — if `stoppingToken` is signaled mid-batch, you want to finish soon, not be stuck for minutes.
4. **Use `try/finally`** to ensure cleanup logic (closing files, releasing locks) always runs, cancellation or not.
5. **Tune `HostOptions.ShutdownTimeout`** to give genuinely long-running units of work enough time to wrap up — but not so long that deployments/restarts hang.
6. **Avoid swallowing `OperationCanceledException` silently everywhere** — log it once at the top level so you have visibility that a shutdown-triggered exit (vs. a real crash) occurred.