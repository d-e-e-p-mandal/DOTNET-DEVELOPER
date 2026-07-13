# 10. Task Parallel Library (TPL)

## `Task`

`System.Threading.Tasks.Task` represents an asynchronous operation. It's the foundation for `async`/`await` and most concurrency in modern .NET.

```csharp
Task task = Task.Run(() => DoWork());
await task;
```

`Task<T>` represents an asynchronous operation that returns a value of type `T`.

```csharp
Task<int> task = Task.Run(() => ComputeValue());
int result = await task;
```

## `Task.Run()`

Schedules a delegate to run on the thread pool, returning a `Task` (or `Task<T>`) representing its completion.

```csharp
await Task.Run(() =>
{
    // CPU-bound work that benefits from running off the calling thread
    HeavyComputation();
});
```

⚠️ Don't use `Task.Run` to wrap something that's *already* naturally asynchronous (like `HttpClient.GetAsync`) — just `await` it directly. `Task.Run` is for pushing **synchronous, CPU-bound** work onto a background thread.

## `Task.Factory`

The older, more configurable way to create tasks, offering more control (e.g., specifying a `TaskCreationOptions` or a custom `TaskScheduler`).

```csharp
Task t = Task.Factory.StartNew(() => DoWork(), TaskCreationOptions.LongRunning);
```

`TaskCreationOptions.LongRunning` hints to the scheduler that this task will run for a while, which can cause it to be given a dedicated thread rather than a typical pooled one — useful for genuinely long-lived loop-style work, though `BackgroundService.ExecuteAsync` (an async method) generally doesn't need this since it's not occupying a thread while awaiting.

## `ContinueWith()`

Attaches a continuation to run after a task completes — predecessor to `async`/`await`, rarely needed directly now, but still seen in legacy code or advanced scheduling scenarios.

```csharp
Task.Run(() => DoWork())
    .ContinueWith(t =>
    {
        if (t.IsFaulted) Console.WriteLine("Failed: " + t.Exception);
        else Console.WriteLine("Done");
    });
```

Prefer `try/catch` around `await` in modern code instead of `ContinueWith` for error handling.

---

## Task Status

A `Task` moves through a well-defined set of states, exposed via `task.Status`:

| Status | Meaning |
|---|---|
| `Created` | Task object created but not yet scheduled to run |
| `WaitingToRun` | Scheduled, waiting for a thread pool thread to become available |
| `Running` | Actively executing |
| `RanToCompletion` (often grouped under "Completed") | Finished successfully |
| `Faulted` | Finished with an unhandled exception |
| `Canceled` | Finished due to cancellation (`OperationCanceledException` from a linked token) |

```csharp
Task t = Task.Run(() => throw new Exception("Oops"));
try { await t; } catch { }
Console.WriteLine(t.Status); // Faulted
Console.WriteLine(t.Exception); // AggregateException wrapping the original
```

In Background Services, checking `Status`/`IsFaulted`/`IsCanceled` is occasionally useful when manually managing multiple concurrent tasks (e.g., `Task.WhenAll` over several parallel jobs), to determine which ones failed and why.

---

## Task Scheduling

### `TaskScheduler`
Determines *how and where* a task's code actually runs (which thread, with what concurrency limits). The default is `TaskScheduler.Default`, which queues work to the `ThreadPool`.

```csharp
Task.Factory.StartNew(() => DoWork(), CancellationToken.None, TaskCreationOptions.None, TaskScheduler.Default);
```

Custom schedulers exist for niche cases (e.g., limiting concurrency to N at a time, or marshaling work back onto a specific UI thread — irrelevant for headless Background Services, but you might encounter `ConcurrentExclusiveSchedulerPair` for advanced concurrency control).

### Thread Pool Integration
By default, `Task`s are scheduled onto the `ThreadPool`. This is exactly why "Task" and "ThreadPool" sections are so closely related: every `Task.Run()` call is essentially "queue this delegate onto the thread pool and give me a handle (`Task`) to track its completion."

---

## TPL Patterns Relevant to Background Services

### Running Parallel Work Inside `ExecuteAsync`
```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        var tasks = pendingItems.Select(item => ProcessItemAsync(item, stoppingToken));
        await Task.WhenAll(tasks); // run all in parallel, wait for all to finish

        await Task.Delay(TimeSpan.FromSeconds(30), stoppingToken);
    }
}
```

### Limiting Parallelism with `SemaphoreSlim` (preview — full detail in Advanced Concurrency)
```csharp
var semaphore = new SemaphoreSlim(5); // max 5 concurrent
var tasks = items.Select(async item =>
{
    await semaphore.WaitAsync(stoppingToken);
    try { await ProcessItemAsync(item, stoppingToken); }
    finally { semaphore.Release(); }
});
await Task.WhenAll(tasks);
```

### `Task.WhenAny()` for Racing/Timeout Patterns
```csharp
var workTask = DoLongRunningWorkAsync(stoppingToken);
var timeoutTask = Task.Delay(TimeSpan.FromMinutes(5), stoppingToken);

var completed = await Task.WhenAny(workTask, timeoutTask);
if (completed == timeoutTask)
{
    _logger.LogWarning("Work timed out!");
}
```

These patterns are foundational for batch processing (process many items concurrently with bounded parallelism) and for "Performance Optimization" topics covered later (batching, parallel processing of independent units of work).