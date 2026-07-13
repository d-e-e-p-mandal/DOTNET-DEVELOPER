# 13. Timers

## `PeriodicTimer` (Modern, Recommended — .NET 6+)

An `async`-friendly timer purpose-built for loop-style periodic work, like background services.

```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    using var timer = new PeriodicTimer(TimeSpan.FromSeconds(30));

    while (await timer.WaitForNextTickAsync(stoppingToken))
    {
        await DoWorkAsync(stoppingToken);
    }
}
```

### Why It's Preferred
- `WaitForNextTickAsync` returns a `ValueTask<bool>` — `true` while ticking normally, `false`/throws `OperationCanceledException` when the token is cancelled — making the loop condition naturally cancellation-aware.
- Does **not** queue up multiple overlapping ticks if your work takes longer than the interval — it waits for the current work to finish, then waits for the *next* interval boundary, avoiding unbounded overlap.
- No drift accumulation issue like manually summing `Task.Delay` durations across iterations with varying work time, since each call to `WaitForNextTickAsync` is relative to the last tick (similar idea to `System.Threading.Timer`, but `async`-native).
- Properly disposed via `using` — releases internal timer resources.

---

## `System.Threading.Timer`

An older, callback-based timer that fires a delegate periodically on a thread-pool thread — independent of `async`/`await`.

```csharp
public class OldStyleHostedService : IHostedService, IDisposable
{
    private Timer? _timer;

    public Task StartAsync(CancellationToken cancellationToken)
    {
        _timer = new Timer(DoWork, null, dueTime: TimeSpan.Zero, period: TimeSpan.FromSeconds(10));
        return Task.CompletedTask;
    }

    private void DoWork(object? state)
    {
        Console.WriteLine($"Tick at {DateTime.Now}");
        // NOTE: this callback can overlap with itself if work takes longer than the period!
    }

    public Task StopAsync(CancellationToken cancellationToken)
    {
        _timer?.Change(Timeout.Infinite, 0);
        return Task.CompletedTask;
    }

    public void Dispose() => _timer?.Dispose();
}
```

⚠️ **Overlap risk**: `System.Threading.Timer` will fire the callback again at the next interval **even if the previous callback hasn't finished**, potentially running multiple instances concurrently — you must guard against this yourself (e.g., a `lock`/flag) if your work can run longer than the interval. `PeriodicTimer` avoids this naturally because you control the loop with `await`.

## `Task.Delay()`

The simplest periodic pattern — used directly inside a `while` loop.

```csharp
while (!stoppingToken.IsCancellationRequested)
{
    DoWork();
    await Task.Delay(TimeSpan.FromSeconds(10), stoppingToken);
}
```

### Drift Consideration
If `DoWork()` itself takes meaningful time, the *actual* interval between work starts is `work duration + delay duration`, not exactly the delay duration — this can drift over many iterations. `PeriodicTimer` has the same "wait after work" characteristic by default (it's not wall-clock-anchored either, unless you measure and adjust manually) — if you need strict wall-clock anchoring (e.g., "always run at the top of the minute"), compute the delay to the next boundary explicitly, as shown below.

## Cron Scheduling

`BackgroundService` + `Task.Delay`/`PeriodicTimer` only gives you fixed intervals — not real cron expressions like "every weekday at 9 AM" or "every 15 minutes between 8 AM–6 PM." For true cron-style scheduling:
- Roll your own "next run time" calculation (fine for simple daily/weekly schedules).
- Use **Quartz.NET** or **Hangfire** for full cron expression support (detailed examples in the Background-Job-Patterns and Enterprise sections).

---

## Scheduling Patterns

### Every Minute / Every N Seconds
```csharp
using var timer = new PeriodicTimer(TimeSpan.FromMinutes(1));
while (await timer.WaitForNextTickAsync(stoppingToken))
{
    await DoWorkAsync(stoppingToken);
}
```

### Every Hour, Anchored to the Clock (e.g., always at :00)
```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        var now = DateTime.Now;
        var nextHour = now.Date.AddHours(now.Hour + 1);
        var delay = nextHour - now;

        await Task.Delay(delay, stoppingToken);
        await DoHourlyWorkAsync(stoppingToken);
    }
}
```

### Daily Jobs (e.g., every day at 2:00 AM)
```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        var now = DateTime.Now;
        var nextRun = now.Date.AddHours(2);
        if (now >= nextRun) nextRun = nextRun.AddDays(1);

        var delay = nextRun - now;
        await Task.Delay(delay, stoppingToken);

        await RunDailyJobAsync(stoppingToken);
    }
}
```

### Weekly Jobs (e.g., every Monday at 6 AM)
```csharp
protected override async Task ExecuteAsync(CancellationToken stoppingToken)
{
    while (!stoppingToken.IsCancellationRequested)
    {
        var now = DateTime.Now;
        int daysUntilMonday = ((int)DayOfWeek.Monday - (int)now.DayOfWeek + 7) % 7;
        var nextMonday = now.Date.AddDays(daysUntilMonday == 0 ? 7 : daysUntilMonday).AddHours(6);

        var delay = nextMonday - now;
        await Task.Delay(delay, stoppingToken);

        await RunWeeklyJobAsync(stoppingToken);
    }
}
```

### Cron Expression with Quartz.NET (Real Cron Support)
```csharp
builder.Services.AddQuartz(q =>
{
    q.AddJob<DailyReportJob>(opts => opts.WithIdentity("dailyReportJob"));
    q.AddTrigger(opts => opts
        .ForJob("dailyReportJob")
        .WithCronSchedule("0 0 2 * * ?")); // every day at 2:00 AM
});
builder.Services.AddQuartzHostedService();
```

Cron expression format (Quartz uses 6/7-field format including seconds): `seconds minutes hours day-of-month month day-of-week [year]`.

## Choosing the Right Timer Approach

| Need | Recommended Tool |
|---|---|
| Simple fixed interval (every N seconds/minutes) | `PeriodicTimer` |
| Legacy/callback style, non-async codebase | `System.Threading.Timer` |
| Anchored to specific wall-clock times (daily/weekly) | Manual "next run" calculation + `Task.Delay` |
| Complex schedules, multiple jobs, persistence, dashboards | Quartz.NET or Hangfire |