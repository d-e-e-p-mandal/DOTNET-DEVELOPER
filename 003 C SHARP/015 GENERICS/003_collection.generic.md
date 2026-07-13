# Generic Class :

**Directive :**
```cs
using System.Collections.Generic;
```

**Generic Class with Multiple Types :**
```cs
class Pair<T, U>
{
    public T First;
    public U Second;
}
```
Example:
```cs
Pair<int, string> p = new Pair<int, string>();
p.First = 1;
p.Second = "One";
```

**Generic Collections :**
```cs
using System.Collections.Generic;

List<int> list = new List<int>();
list.Add(10);
list.Add(20);

Dictionary<int, string> dict = new Dictionary<int, string>();
dict.Add(1, "One");
```
**Common Generic Collections :**
	•	List
	•	Dictionary<TKey, TValue>
	•	Stack
	•	Queue
	•	HashSet