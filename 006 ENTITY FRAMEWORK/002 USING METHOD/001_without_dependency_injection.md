# Without Dependency Injection

## What Happens?

- You create the object yourself using `new`.
- ASP.NET Core does not create the object.
- You manage the object manually.

Simple Meaning:

```text
I Create Object Myself
```

---

## Example

```cs
var context = new AppDbContext();
```

---

## Usage

```cs
var context = new AppDbContext();

var employees = context.Employees.ToList();
```

---

## Flow

```text
Program
    ↓
new AppDbContext()
    ↓
Object Created
    ↓
Use Object
```

---

## Responsibilities

You must:

- Create object
- Manage object
- Dispose object

Example:

```cs
using var context = new AppDbContext();

var employees = context.Employees.ToList();
```

---

## Drawbacks

- More Code
- Manual Management
- Hard To Test
- Tight Coupling

---

## Where Commonly Used?

```text
Console Applications

Small Programs

Learning Examples

Quick Testing
```

---

## Quick Revision

```text
Without DI
      ↓
new AppDbContext()
      ↓
Manual Object Creation
      ↓
Manual Disposal
      ↓
Use Object
```