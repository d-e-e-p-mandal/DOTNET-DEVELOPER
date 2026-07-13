

# 4. IOptionsSnapshot<T>

## Purpose

Reload configuration per request.

Used In:

```text
Web Applications
```

---

## Injection

```cs
public EmployeeService(
    IOptionsSnapshot<ApiSettings>
        options)
{
}
```

---

## Lifetime

```text
Scoped
```

---

# 5. IOptionsMonitor<T>

## Purpose

Detect configuration changes automatically.

Used For:

```text
Long Running Services

Background Services

Worker Services
```

---

## Injection

```cs
public EmployeeService(
    IOptionsMonitor<ApiSettings>
        options)
{
}
```

---

## Current Value

```cs
options.CurrentValue
```

---

## OnChange

```cs
options.OnChange(
    settings =>
    {
        Console.WriteLine(
            settings.ApiKey);
    });
```

---

# Comparison

| Type | Purpose |
|--------|----------|
| IConfiguration | Read Values Directly |
| ConfigHelper | Centralized Logic |
| IOptions<T> | Strongly Typed Settings |
| IOptionsSnapshot<T> | Per Request Reload |
| IOptionsMonitor<T> | Auto Reload On Change |

---

# Most Common Industry Usage

## Small Project

```text
IConfiguration
```

---

## Medium Project

```text
ConfigHelper
```

---
