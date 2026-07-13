
## Boxing and Generics

**Without Generics:**
```cs
ArrayList list = new ArrayList();
list.Add(10);   // boxing
```

**With Generics:**
```cs
List<int> list = new List<int>();
list.Add(10);   // no boxing
```

**Explanation :**
- Non-generic box → can store anything (confusing)
- Generic box → stores only one type (safe)