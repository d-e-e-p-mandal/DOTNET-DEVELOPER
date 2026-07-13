

# Using CreateScope()

Used when working directly inside:

```text
Program.cs

BackgroundService

Worker Service
```

---

## Registration

```cs
builder.Services.AddDbContext<
    AppDbContext>();
```

---

## Get Object From DI Container

```cs
using var scope =
    app.Services.CreateScope();

var context =
    scope.ServiceProvider
         .GetRequiredService<
             AppDbContext>();
```

---

## Usage

```cs
using var scope =
    app.Services.CreateScope();

var context =
    scope.ServiceProvider
         .GetRequiredService<
             AppDbContext>();

var employees =
    context.Employees.ToList();
```

---

## Flow

```text
Program
    ↓
CreateScope()
    ↓
GetRequiredService()
    ↓
AppDbContext Created
    ↓
Use Object
```

---

## Commonly Used In
- Program.cs
- Background Service
- Worker Service
- Console Application


```text
CreateScope()
    ↓
GetRequiredService()

Used In
    ↓
Program.cs
Worker Service
```