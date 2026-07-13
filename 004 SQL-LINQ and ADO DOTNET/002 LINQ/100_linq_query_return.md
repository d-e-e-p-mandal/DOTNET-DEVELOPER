# IQueryable<T>

```cs
public IQueryable<Employee> Get()
{
    return _context.Employees;
}
```

## Meaning

```text
Return Query Only
```

## Query Not Executed

```cs
return _context.Employees;
```

Only returns query.

Database is not hit yet.

---

## Query Executes Here

```cs
var employees = repository.Get()
                          .Where(x => x.Id > 5)
                          .ToList();
```

`ToList()` executes query.

---

## Generated SQL

```sql
SELECT *
FROM Employees
WHERE Id > 5
```

---

## Why Use IQueryable?

- Return query only
- Allow filtering later
- Allow sorting later
- Allow paging later
- Better performance

---

## Repository Example

```cs
public IQueryable<Employee> GetAll()
{
    return _context.Employees;
}
```

---

## Service Example

```cs
var employees =
    _repository.GetAll()
               .Where(x => x.IsActive);
```

Query still not executed.

---

## Execution

```cs
var result = employees.ToList();
```

Now SQL executes.

---

## Simple Note

```text
IQueryable
      ↓
Return Query
      ↓
Add Conditions
      ↓
Execute Later
```

---

## Industry Use

Mostly used when:
- Entity Framework
- Filtering
- Sorting
- Pagination
- Search APIs

---

## If Only Query Needed

Use:

```cs
IQueryable<T>
```

Do not use:

```cs
IEnumerable<T>
```

because IQueryable is specifically designed for returning database queries.