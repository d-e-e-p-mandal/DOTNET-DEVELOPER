# Task Members in .NET
- Most async methods return:

```cs
Task
```
or

```cs
Task<T>
```

Example:

```cs
Task<HttpResponseMessage> task = client.GetAsync("api/employees");
```

---

## await

### Purpose

Waits asynchronously for task completion.

### Recommended

```cs
HttpResponseMessage response = await client.GetAsync("api/employees");
```

### Meaning
- Wait For Result
- Without Blocking Thread


---

## Result

### Purpose

Gets task result.

### Example

```cs
HttpResponseMessage response = client.GetAsync("api/employees").Result;
```

### Meaning

```text
Wait For Completion
Then Return Result
```

### Note

```text
Blocks Current Thread
```

Not recommended in ASP.NET Core.

---

## Wait()

### Purpose

Wait for task completion.

### Example

```cs
client.GetAsync("api/employees").Wait();
```

### Meaning

```text
Pause Current Thread
Until Task Completes
```

### Return

```cs
void
```

---

## GetAwaiter().GetResult()

### Purpose

Get result synchronously.

### Example

```cs
HttpResponseMessage response =
    client.GetAsync(
        "api/employees")
        .GetAwaiter()
        .GetResult();
```

### Meaning

```text
Wait For Completion
Then Return Result
```

---

## Status

### Purpose

Check current task state.

### Example

```cs
var task =
    client.GetAsync("api/employees");

Console.WriteLine(task.Status);
```

### Possible Values

```text
Created

WaitingForActivation

Running

RanToCompletion

Canceled

Faulted
```

---

## IsCompleted

### Purpose

Check whether task finished.

### Example

```cs
bool completed = task.IsCompleted;
```

### Output

```text
true
false
```

---

## IsCanceled

### Purpose

Check whether task was canceled.

### Example

```cs
bool canceled = task.IsCanceled;
```

### Output

```text
true
false
```

---

## IsFaulted

### Purpose

Check whether task failed.

### Example

```cs
bool failed = task.IsFaulted;
```

### Output

```text
true
false
```

---

## Exception

### Purpose

Get exception from failed task.

### Example

```cs
Exception ex = task.Exception;
```

### Used When

```text
Task Failed

Task Faulted
```

---

# Quick Revision

| Member | Purpose |
|----------|----------|
| await | Wait asynchronously |
| Result | Get result synchronously |
| Wait() | Wait for completion |
| GetAwaiter().GetResult() | Get result synchronously |
| Status | Current task state |
| IsCompleted | Task finished? |
| IsCanceled | Task canceled? |
| IsFaulted | Task failed? |
| Exception | Error information |

---

# Most Common Usage

```cs
await task;
```

```cs
task.Result;
```

```cs
task.Wait();
```

```cs
task.GetAwaiter().GetResult();
```

Recommended:

```cs
await task;
```