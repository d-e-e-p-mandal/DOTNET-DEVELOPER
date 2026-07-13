# Collections in C#

---

# What are Collections?

A **Collection** is a group of objects stored together.

Collections are used to store, manage, search, insert, update, and delete data efficiently.

Most collections are available in the following namespaces:

```csharp
using System.Collections;
using System.Collections.Generic;
```

---

# Why Use Collections?

Collections provide many advantages over arrays.

- Dynamic Size
- Easy Insertion
- Easy Deletion
- Searching
- Sorting
- Better Memory Management
- Built-in Methods

---

# Types of Collections

## Non-Generic Collection

Stores any type of object.

Example

- ArrayList
- Hashtable
- Queue
- Stack

Namespace

```csharp
using System.Collections;
```

---

## Generic Collection

Stores only one specific data type.

Example

- List<T>
- Dictionary<TKey, TValue>
- Stack<T>
- Queue<T>
- HashSet<T>
- LinkedList<T>

Namespace

```csharp
using System.Collections.Generic;
```

---

# ArrayList

An **ArrayList** is a dynamic array that can store objects of different data types.

It automatically increases its size when new elements are added.

## Features

- Dynamic Size
- Stores Different Data Types
- Indexed Collection
- Non-Generic
- Slower than Generic Collections because of Boxing and Unboxing

## Creating an ArrayList

```csharp
using System.Collections;

ArrayList list = new ArrayList();
```

## Example

```csharp
using System.Collections;

ArrayList list = new ArrayList();

list.Add(10);
list.Add("John");
list.Add(3.14);

foreach(var item in list)
{
    Console.WriteLine(item);
}
```

## Common Methods

- Add()
- AddRange()
- Remove()
- RemoveAt()
- RemoveRange()
- Insert()
- InsertRange()
- Clear()
- Contains()
- IndexOf()
- Sort()
- Reverse()

## Properties

- Count
- Capacity

---

# List<T>

A **List<T>** is a generic version of ArrayList.

It stores only one data type and grows automatically.

## Features

- Dynamic Size
- Type Safe
- Fast
- Supports Indexing
- Most Commonly Used Collection

## Creating a List

```csharp
List<int> numbers = new List<int>();
```

## Example

```csharp
List<int> numbers = new List<int>();

numbers.Add(10);
numbers.Add(20);
numbers.Add(30);

foreach(int item in numbers)
{
    Console.WriteLine(item);
}
```

## Common Methods

- Add()
- AddRange()
- Insert()
- InsertRange()
- Remove()
- RemoveAt()
- RemoveAll()
- RemoveRange()
- Clear()
- Contains()
- Exists()
- Find()
- FindAll()
- FindIndex()
- IndexOf()
- LastIndexOf()
- BinarySearch()
- Sort()
- Reverse()
- CopyTo()
- ToArray()

## Properties

- Count
- Capacity

---

# LinkedList<T>

A **LinkedList<T>** stores elements as nodes.

Each node contains:

- Data
- Reference to Next Node
- Reference to Previous Node

It is a **Doubly Linked List**.

## Features

- Dynamic
- Fast Insertion
- Fast Deletion
- No Index

## Creating

```csharp
LinkedList<int> list = new LinkedList<int>();
```

## Example

```csharp
LinkedList<int> list = new LinkedList<int>();

list.AddLast(10);
list.AddLast(20);
list.AddFirst(5);

foreach(int item in list)
{
    Console.WriteLine(item);
}
```

## Common Methods

- AddFirst()
- AddLast()
- AddAfter()
- AddBefore()
- Remove()
- RemoveFirst()
- RemoveLast()
- Find()
- FindLast()
- Contains()
- Clear()

## Properties

- First
- Last
- Count

---

# Stack<T>

A **Stack** stores data using the **LIFO (Last In First Out)** principle.

Example

```
Top
30
20
10
```

## Features

- LIFO
- Fast Insert/Delete
- Only Top Element Accessible

## Creating

```csharp
Stack<int> stack = new Stack<int>();
```

## Example

```csharp
Stack<int> stack = new Stack<int>();

stack.Push(10);
stack.Push(20);
stack.Push(30);

Console.WriteLine(stack.Pop());
Console.WriteLine(stack.Peek());
```

## Common Methods

- Push()
- Pop()
- Peek()
- Contains()
- Clear()
- ToArray()

## Properties

- Count

---

# Queue<T>

A **Queue** follows the **FIFO (First In First Out)** principle.

Example

```
Front → 10 20 30 ← Rear
```

## Features

- FIFO
- Fast Insert/Delete

## Creating

```csharp
Queue<int> queue = new Queue<int>();
```

## Example

```csharp
Queue<int> queue = new Queue<int>();

queue.Enqueue(10);
queue.Enqueue(20);
queue.Enqueue(30);

Console.WriteLine(queue.Dequeue());
Console.WriteLine(queue.Peek());
```

## Common Methods

- Enqueue()
- Dequeue()
- Peek()
- Contains()
- Clear()
- ToArray()

## Properties

- Count

---

# Dictionary<TKey, TValue>

A **Dictionary** stores data as **Key-Value** pairs.

Each key must be unique.

Example

```
101 → John
102 → Alice
103 → Bob
```

## Features

- Key-Value Pair
- Unique Keys
- Fast Searching
- Generic Collection

## Creating

```csharp
Dictionary<int,string> students = new Dictionary<int,string>();
```

## Example

```csharp
Dictionary<int,string> students = new Dictionary<int,string>();

students.Add(101,"John");
students.Add(102,"Alice");

foreach(var item in students)
{
    Console.WriteLine(item.Key + " " + item.Value);
}
```

## Common Methods

- Add()
- Remove()
- ContainsKey()
- ContainsValue()
- TryGetValue()
- Clear()

## Properties

- Keys
- Values
- Count

---

# HashSet<T>

A **HashSet** stores only **unique values**.

Duplicate values are not allowed.

## Features

- No Duplicate Elements
- Unordered Collection
- Fast Searching
- Generic Collection

## Creating

```csharp
HashSet<int> numbers = new HashSet<int>();
```

## Example

```csharp
HashSet<int> numbers = new HashSet<int>();

numbers.Add(10);
numbers.Add(20);
numbers.Add(10);

foreach(int item in numbers)
{
    Console.WriteLine(item);
}
```

Output

```
10
20
```

## Common Methods

- Add()
- Remove()
- Contains()
- Clear()
- UnionWith()
- IntersectWith()
- ExceptWith()
- SymmetricExceptWith()
- IsSubsetOf()
- IsSupersetOf()

## Properties

- Count

---

# Collection Comparison

| Collection | Duplicate | Ordered | Indexed | Dynamic |
|------------|-----------|----------|---------|---------|
| ArrayList | Yes | Yes | Yes | Yes |
| List<T> | Yes | Yes | Yes | Yes |
| LinkedList<T> | Yes | Yes | No | Yes |
| Stack<T> | Yes | LIFO | No | Yes |
| Queue<T> | Yes | FIFO | No | Yes |
| Dictionary<TKey,TValue> | Keys No | No | No | Yes |
| HashSet<T> | No | No | No | Yes |

---

# Which Collection Should You Use?

| Requirement | Collection |
|-------------|------------|
| Dynamic Array | List<T> |
| Mixed Data Types | ArrayList |
| Fast Insert/Delete | LinkedList<T> |
| Last In First Out | Stack<T> |
| First In First Out | Queue<T> |
| Key-Value Storage | Dictionary<TKey, TValue> |
| Unique Values | HashSet<T> |

---
