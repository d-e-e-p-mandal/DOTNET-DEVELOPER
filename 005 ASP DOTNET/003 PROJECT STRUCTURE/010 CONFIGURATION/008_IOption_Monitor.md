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
