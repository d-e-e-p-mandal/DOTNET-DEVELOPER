
# WHERE TO USE async/await 

- Rule: Use it for I/O-bound operations (waiting tasks)

### 1. Database Operations

**Using Entity Framework Core :**
* ToListAsync()
* FirstOrDefaultAsync()
* SaveChangesAsync()
* FindAsync()

**When:**
* Fetching data
* Saving/updating records


### 2. HTTP / API Calls

**Using HttpClient :**
* GetAsync()
* PostAsync()
* SendAsync()
* ReadAsStringAsync()

**When:**
* Calling external APIs
* Microservices communication


### 3. File Operations (I/O)
* ReadAllTextAsync()
* WriteAllTextAsync()
* ReadAllBytesAsync()
* WriteAllBytesAsync()

**When :**
* Reading/writing files
* Upload/download

### 4. Stream Operations
* ReadAsync()
* WriteAsync()
* CopyToAsync()

**When :**
* Large file handling
* Network streaming


### 5. Web API Controllers (Custome Function)

**Using ASP.NET Core :**
```cs
public async Task<IActionResult> Get()
{
    var data = await service.GetAsync();
    return Ok(data);
}
```
**When :**
* Calling DB or services inside APIs


### 6. Background Services / Workers
* ExecuteAsync()
* Task.Delay()

**When :**
* Scheduled jobs
* Queue processing


### 7. Parallel Task Execution
* Task.WhenAll()
* Task.WhenAny()

**When :**
* Running multiple independent tasks

### 8. Timers / Delays

* Task.Delay()

**When :**
* Non-blocking wait


### 9. Real-time Apps (SignalR)

* SendAsync()

**When :**
* Chat apps
* Notifications

### 10. Third-party SDKs

**Examples :**
* Azure SDK
* Firebase
* Payment APIs

- If SDK provides async → use await

### 11. Asynchronous LINQ (DB only)
```cs
await _context.Users.ToListAsync();
```
**when :**
* Query runs on database

### 12. Task-based Methods

* Task.Run() (for background execution)

---------------------------------------------


🔷 PART 2 — WHEN NOT TO USE async/await

👉 Rule: Avoid for CPU-bound / instant operations

⸻

🔴 1. CPU-bound Work

int result = Calculate();

❌ Don’t use async

✔ If needed:

await Task.Run(() => Calculate());

⸻

🔴 2. Simple Methods

int Add(int a, int b) => a + b;

⸻

🔴 3. In-memory LINQ

var data = list.Where(x => x > 5);

⸻

🔴 4. Constructors ❌

// Not allowed
public async MyClass() { }

⸻

🔴 5. Property Getters/Setters

public int Value { get; set; }

⸻

🔴 6. When No Await Exists

public async Task Test()
{
    // no await
}

✔ Better:

return Task.CompletedTask;

⸻

🔴 7. Blocking Calls (Wrong Usage)

var result = task.Result;
task.Wait();

❌ Causes deadlocks

⸻

🔴 8. Loops Without Need

foreach(var item in list)
{
    await Process(item);
}

👉 Use Task.WhenAll() if independent

⸻

🔴 9. Pure Synchronous Libraries

👉 If no async API → don’t force it

⸻

🔷 PART 3 — SPECIAL CASES

⸻

🟡 1. async void

✔ Use ONLY for:

* Event handlers

private async void Button_Click(object sender, EventArgs e)

⸻

🟡 2. Interface Requirement

public Task DoWorkAsync()
{
    return Task.CompletedTask;
}

⸻

🟡 3. Fire-and-forget (Careful)

_ = Task.Run(() => Work());

⸻

🔷 FINAL QUICK REVISION

⸻

✅ USE async/await

* Database
* API calls
* File handling
* Streams
* Background tasks
* Parallel tasks

⸻

❌ DO NOT USE

* CPU calculations
* Simple methods
* Constructors
* In-memory operations

⸻

🔥 ONE LINE RULE (VERY IMPORTANT)

👉 If your code is waiting → use async/await
👉 If your code is computing → don’t use it

⸻

If you want next:

* Deadlock explanation (very important for interviews)
* Difference: Task, ValueTask, async void
* Real project structure (MERN + .NET style)

Just tell 👍