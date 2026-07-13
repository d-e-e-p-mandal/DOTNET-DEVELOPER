# C# / .NET Date & Time Format Symbols

## Day Formats

- `d` → Day without leading zero (1–31)
- `dd` → Day with leading zero (01–31)
- `ddd` → Short day name (Mon, Tue)
- `dddd` → Full day name (Monday, Tuesday)

---

## Month Formats

- `M` → Month without leading zero (1–12)
- `MM` → Month with leading zero (01–12)
- `MMM` → Short month name (Jan, Feb)
- `MMMM` → Full month name (January, February)

---

## Year Formats

- `y` → Year minimum digits
- `yy` → Two-digit year (24)
- `yyy` → Three-digit year
- `yyyy` → Four-digit year (2024)
- `yyyyy` → Five-digit year

---

## Hour Formats

### 12-Hour Format

- `h` → Hour without leading zero (1–12)
- `hh` → Hour with leading zero (01–12)

### 24-Hour Format

- `H` → Hour without leading zero (0–23)
- `HH` → Hour with leading zero (00–23)

---

## Minute Formats

- `m` → Minute without leading zero
- `mm` → Minute with leading zero

---

## Second Formats

- `s` → Second without leading zero
- `ss` → Second with leading zero

---

## Fractional Seconds

- `f`
- `ff`
- `fff`
- `ffff`
- `fffff`
- `ffffff`
- `fffffff`

Example:
```text
15:30:45.123
```

---

## AM / PM Formats

- `t` → A / P
- `tt` → AM / PM

---

## Time Zone Formats

- `z`
- `zz`
- `zzz`

Example:
```text
+5
+05
+05:30
```

---

## Date Separators

- `/` → Date separator
- `:` → Time separator

---

## Common Date Formats

### Date Only

```text
dd/MM/yyyy
```

```text
MM/dd/yyyy
```

```text
yyyy-MM-dd
```

```text
dd-MMM-yyyy
```

```text
dd MMMM yyyy
```

---

### Date & Time

```text
dd/MM/yyyy HH:mm:ss
```

```text
yyyy-MM-dd HH:mm:ss
```

```text
dd-MMM-yyyy hh:mm tt
```

---

## Standard DateTime Formats

- `d` → Short Date
- `D` → Long Date
- `t` → Short Time
- `T` → Long Time
- `f` → Full Date + Short Time
- `F` → Full Date + Long Time
- `g` → General Date + Short Time
- `G` → General Date + Long Time
- `M` / `m` → Month Day Pattern
- `Y` / `y` → Year Month Pattern
- `O` / `o` → Round-trip Format
- `R` / `r` → RFC1123 Format
- `s` → Sortable DateTime
- `u` → Universal Sortable DateTime
- `U` → Universal Full DateTime

---

## Most Used Formats

- `dd/MM/yyyy`
- `MM/dd/yyyy`
- `yyyy-MM-dd`
- `dd-MMM-yyyy`
- `dd/MM/yyyy HH:mm:ss`
- `hh:mm tt`
- `HH:mm:ss`
- `yyyy-MM-ddTHH:mm:ss`