# 8. Threading Fundamentals

## Process
A **process** is an instance of a running program — it has its own memory space, handles, and at least one thread. Your .NET application (e.g., `MyWorkerApp.exe`) runs as one OS process.

## Thread
A **thread** is the smallest unit of execution within a process. A process can have multiple threads, all sharing the same memory space (heap), but each with its own stack and execution pointer. Threads let a process do multiple things "at once" (truly parallel on multi-core CPUs, or interleaved via context-switching on a single core).

## Managed Thread
A **managed thread** is a thread that the .NET runtime (CLR) is aware of and manages — represented by the `System.Threading.Thread` class. The CLR maps managed threads onto underlying OS threads. Most of the time in modern .NET, you don't create `Thread` objects directly — you use `Task`/`async`/`ThreadPool`, which manage threads for you under the hood.

## Background Thread vs Foreground Thread

```csharp
Thread t = new Thread(DoWork);
t.IsBackground = true; // background thread
t.Start();
```

- **Foreground thread**: keeps the *process* alive. The CLR will not let the process exit while any foreground thread is still running.
- **Background thread**: does NOT keep the process alive. When all foreground threads finish, the process exits immediately, even if background threads are still mid-execution (they're simply terminated).

By default:
- The main thread of an app is a foreground thread.
- Threads from the `ThreadPool` (which underlies `Task`) are background threads.

⚠️ Note: this OS/CLR-level "background thread" concept is a *different* meaning of "background" than "Background Service" (the hosting feature). A `BackgroundService`'s `ExecuteAsync` code typically runs on `ThreadPool` threads (background threads in the CLR sense), but it's the **host** that keeps the *process* alive for as long as it's running — not thread foreground/background status.

## Thread Lifecycle

```
Unstarted → Running → (Waiting/Sleeping/Blocked) → Running → Stopped
```

- **Unstarted**: `Thread` object created but `.Start()` not called yet.
- **Running**: actively executing or ready to execute (scheduled by the OS).
- **WaitSleepJoin**: blocked — waiting on `Thread.Sleep()`, a lock, `Thread.Join()`, or an I/O operation.
- **Stopped**: the thread's method has returned, or it was aborted.

```csharp
Console.WriteLine(t.ThreadState); // Unstarted, Running, WaitSleepJoin, Stopped, etc.
```

---

## Multithreading

Writing code that uses multiple threads to do work concurrently.

### `Thread` Class — Direct, Low-Level Threading

```csharp
Thread worker = new Thread(() =>
{
    Console.WriteLine("Running on a separate thread");
});
worker.Start();
worker.Join(); // wait for it to finish
```

### `Thread.Start()`
Begins execution of the thread on a new OS thread.

### `Thread.Join()`
Blocks the calling thread until the target thread finishes. Useful for waiting on manually created threads, but **not used in async code** (it blocks synchronously — defeats the purpose of `async`/`await`).

### `Thread.Sleep()`
Blocks the **current** thread for a specified duration, synchronously. In async background service code, avoid `Thread.Sleep()` — use `await Task.Delay()` instead, which doesn't block the underlying thread, allowing it to be returned to the pool while waiting.

```csharp
// ❌ Avoid in async background services — blocks the thread:
Thread.Sleep(5000);

// ✅ Correct — frees the thread while waiting:
await Task.Delay(5000, stoppingToken);
```

### Why Raw `Thread` Is Rarely Used Directly Today
Creating raw OS threads is relatively expensive (memory + OS scheduling overhead), and they're not reused. Modern .NET code almost always prefers:
- `Task.Run()` for CPU-bound work needing a thread pool thread.
- `async`/`await` for I/O-bound work needing no dedicated thread while waiting.

Background Services use this model — `ExecuteAsync` is just an `async Task` method, scheduled on the thread pool as needed by the `async` machinery, not a manually managed `Thread`.

---

## Problems in Multithreaded Code

### Race Condition
Occurs when multiple threads access/modify shared state concurrently, and the outcome depends on the unpredictable timing/order of execution.

```csharp
int counter = 0;

void Increment() => counter++; // NOT atomic: read, add, write — can interleave across threads

Parallel.For(0, 100000, i => Increment());
// counter may end up less than 100000 due to race conditions
```

Fix: use `Interlocked.Increment(ref counter)`, locks, or concurrent collections.

### Deadlock
Two or more threads each hold a resource the other needs, and neither can proceed.

```csharp
// Thread A locks obj1 then tries to lock obj2
// Thread B locks obj2 then tries to lock obj1
// → both wait forever
```

Common in async code when **blocking on async calls** (`.Result`, `.Wait()`) combined with a captured `SynchronizationContext` — classic ASP.NET classic deadlock pattern. Generally not an issue in ASP.NET Core / Worker Service apps (no `SynchronizationContext`), but still best avoided by always using `await`.

### Starvation
A thread is perpetually denied the resources/CPU time it needs to proceed, because other threads are continually prioritized ahead of it (e.g., due to unfair locking, or a thread pool saturated with long-running synchronous work).

### Thread Contention
Multiple threads competing for the same lock/resource, causing some threads to wait. High contention degrades performance — even without deadlock/starvation, lots of time is wasted waiting rather than doing useful work.

### Why This Matters for Background Services
A `BackgroundService` loop processing items from a shared queue, or multiple background services touching shared in-memory state (e.g., a shared cache, counter, or dictionary), can hit all of the above if synchronization isn't handled correctly. This is where `lock`, `SemaphoreSlim`, concurrent collections, and `Interlocked` (covered later in Advanced Concurrency) come in.