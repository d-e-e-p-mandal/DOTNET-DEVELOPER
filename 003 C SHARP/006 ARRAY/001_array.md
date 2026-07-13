# Arrays in C#

---

# Arrays

An **array** is a collection of elements of the same data type stored in contiguous memory locations.

Each element is accessed using its **index**.

- Array indexing starts from **0**.
- Array size is fixed after creation.

### Syntax

```csharp
dataType[] arrayName = new dataType[size];
```

### Example

```csharp
int[] numbers = new int[5];

numbers[0] = 10;
numbers[1] = 20;

Console.WriteLine(numbers[0]);
Console.WriteLine(numbers[1]);
```

---

# One Dimensional Array

A one-dimensional array stores elements in a single row.

### Example

```csharp
int[] numbers = { 10, 20, 30, 40, 50 };

for (int i = 0; i < numbers.Length; i++)
{
    Console.WriteLine(numbers[i]);
}
```

### Using foreach

```csharp
int[] numbers = { 1, 2, 3, 4, 5 };

foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

---

# Multi Dimensional Array

A multi-dimensional array stores data in rows and columns.

### Syntax

```csharp
dataType[,] arrayName = new dataType[rows, columns];
```

### Example

```csharp
int[,] matrix =
{
    {1, 2},
    {3, 4}
};

Console.WriteLine(matrix[0, 0]);
Console.WriteLine(matrix[1, 1]);
```

### Output

```text
1
4
```

---

# Jagged Array

A jagged array is an array of arrays.

Each row can have a different number of elements.

### Syntax

```csharp
dataType[][] arrayName = new dataType[size][];
```

### Example

```csharp
int[][] numbers = new int[2][];

numbers[0] = new int[] { 1, 2, 3 };
numbers[1] = new int[] { 10, 20 };

foreach (int[] row in numbers)
{
    foreach (int value in row)
    {
        Console.Write(value + " ");
    }

    Console.WriteLine();
}
```

### Output

```text
1 2 3
10 20
```

---

# Array Methods

Some commonly used array methods are:

| Method | Description |
|---------|-------------|
| `Sort()` | Sorts the array |
| `Reverse()` | Reverses the array |
| `Clear()` | Clears array elements |
| `Copy()` | Copies one array to another |
| `IndexOf()` | Finds the index of an element |
| `Resize()` | Changes the array size |

---

## Array.Sort()

```csharp
int[] numbers = { 5, 2, 4, 1, 3 };

Array.Sort(numbers);

foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

---

## Array.Reverse()

```csharp
int[] numbers = { 1, 2, 3, 4 };

Array.Reverse(numbers);

foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

---

## Array.Clear()

```csharp
int[] numbers = { 10, 20, 30 };

Array.Clear(numbers, 0, 2);

foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

---

## Array.Copy()

```csharp
int[] source = { 10, 20, 30 };
int[] destination = new int[3];

Array.Copy(source, destination, 3);

foreach (int num in destination)
{
    Console.WriteLine(num);
}
```

---

## Array.IndexOf()

```csharp
int[] numbers = { 10, 20, 30 };

int index = Array.IndexOf(numbers, 20);

Console.WriteLine(index);
```

---

## Array.Resize()

```csharp
int[] numbers = { 1, 2, 3 };

Array.Resize(ref numbers, 5);

numbers[3] = 4;
numbers[4] = 5;

foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

---

# Array Class

The `Array` class provides built-in methods to work with arrays.

Some useful members are:

| Member | Description |
|---------|-------------|
| `Length` | Returns total number of elements |
| `Sort()` | Sorts elements |
| `Reverse()` | Reverses elements |
| `Clear()` | Clears elements |
| `Copy()` | Copies arrays |
| `IndexOf()` | Finds an element's index |
| `Resize()` | Changes array size |

### Example

```csharp
int[] numbers = { 5, 3, 1, 4, 2 };

Console.WriteLine(numbers.Length);

Array.Sort(numbers);

foreach (int num in numbers)
{
    Console.WriteLine(num);
}
```

---