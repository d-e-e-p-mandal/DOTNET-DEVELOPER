# 4. Service Lifecycle

## Application Startup Flow

```
Program.cs starts
      │
      ▼
Host.CreateApplicationBuilder() / CreateDefaultBuilder()
      │
      ▼
Services registered (DI container configured)
      │
      ▼
builder.Build()  →  DI Container is built
      │
      ▼
host.Run() / await host.RunAsync()
      │
      ▼
Host starts all registered IHostedService instances
  (StartAsync called, in registration order)
      │
      ▼
BackgroundService.StartAsync()
  → internally kicks off ExecuteAsync() WITHOUT awaiting it
      │
      ▼
ExecuteAsync() runs (your loop/work begins)
      │
      ▼
ApplicationStarted lifecycle event fires
```

## Application Shutdown Flow

```
Shutdown signal received
  (Ctrl+C, SIGTERM, container stop, IHostApplicationLifetime.StopApplication())
      │
      ▼
ApplicationStopping lifecycle event fires
      │
      ▼
Host triggers the shared "stopping" CancellationToken
  → stoppingToken.IsCancellationRequested becomes true
  → any await Task.Delay(..., stoppingToken) immediately throws OperationCanceledException
      │
      ▼
StopAsync() called on each hosted service
  (in REVERSE registration order)
      │
      ▼
BackgroundService.StopAsync():
  - signals cancellation
  - awaits the ExecuteAsync task (with a timeout = HostOptions.ShutdownTimeout)
      │
      ▼
Dispose() called (IDisposable cleanup)
      │
      ▼
ApplicationStopped lifecycle event fires
      │
      ▼
Process exits
```

## Detailed Lifecycle of a `BackgroundService` Instance

1. **Constructor** — runs when the DI container creates the singleton instance (happens once, at host build/start time). Inject all dependencies here (loggers, scoped factories, configuration, etc.) — but remember, the instance itself lives for the app's whole lifetime, so don't inject scoped services directly (see Dependency Injection section).

2. **`StartAsync(CancellationToken)`** — base implementation kicks off `ExecuteAsync` without blocking startup.

3. **`ExecuteAsync(CancellationToken stoppingToken)`** — your actual logic; typically an infinite loop guarded by `stoppingToken`.

4. **`StopAsync(CancellationToken cancellationToken)`** — called during shutdown. The base implementation:
   - Signals the internal `stoppingToken` used inside `ExecuteAsync`.
   - Waits for the `ExecuteAsync` task to finish, or until the shutdown timeout elapses, or until the `cancellationToken` passed to `StopAsync` itself is cancelled (meaning shutdown is taking too long and the host wants to force-exit).

5. **`Dispose()`** — cleans up internal resources (e.g., the internal `CancellationTokenSource`). If you override `Dispose`, always call `base.Dispose()`.

```csharp
public class MyWorker : BackgroundService
{
    public MyWorker(/* dependencies */) { /* 1. Constructor */ }

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        // 3. Main work loop
        while (!stoppingToken.IsCancellationRequested)
        {
            await Task.Delay(1000, stoppingToken);
        }
    }

    public override async Task StopAsync(CancellationToken cancellationToken)
    {
        // 4. Optional custom cleanup before base stops the loop
        Console.WriteLine("Custom cleanup...");
        await base.StopAsync(cancellationToken);
    }

    public override void Dispose()
    {
        // 5. Optional extra disposal
        base.Dispose();
    }
}
```

## `IHostApplicationLifetime`

Inject this to hook into specific lifecycle moments anywhere in your app (not just inside a hosted service):

```csharp
public class MyWorker : BackgroundService
{
    private readonly IHostApplicationLifetime _lifetime;

    public MyWorker(IHostApplicationLifetime lifetime) => _lifetime = lifetime;

    protected override Task ExecuteAsync(CancellationToken stoppingToken)
    {
        _lifetime.ApplicationStarted.Register(() => Console.WriteLine("App started"));
        _lifetime.ApplicationStopping.Register(() => Console.WriteLine("App stopping"));
        _lifetime.ApplicationStopped.Register(() => Console.WriteLine("App stopped"));
        return Task.CompletedTask;
    }
}
```

You can also **trigger** a shutdown programmatically:
```csharp
_lifetime.StopApplication();
```

## Shutdown Timeout Configuration

```csharp
builder.Services.Configure<HostOptions>(options =>
{
    options.ShutdownTimeout = TimeSpan.FromSeconds(30); // default is 5 seconds
});
```

If your `ExecuteAsync` doesn't finish cleaning up within this window after cancellation is requested, the host force-stops it.

## Key Mental Model
Think of the lifecycle as **two parallel timelines**:
- The **host's** lifecycle (start app → run → stop app).
- **Your loop's** lifecycle inside `ExecuteAsync`, which is just a long-running `Task` that the host starts once and waits on once (during shutdown).

Everything about graceful shutdown comes down to: *"Does your loop check `stoppingToken` often enough to exit promptly when asked?"*