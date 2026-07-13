# Strings in C#

---

# What is a String?

A **String** is a sequence of Unicode characters used to store text.

In C#, `string` is a keyword (alias) for the **System.String** class.

```csharp
string message = "Hello World";
```

---

# Characteristics of String

- Reference Type
- Immutable (Cannot be modified after creation)
- Stores Unicode characters
- Zero-based indexing
- Supports indexing using `[]`
- Provides many built-in methods
- Defined in the `System` namespace

---

# Why are Strings Immutable?

When a string is modified, C# creates a **new string object** instead of changing the existing one.

### Example

```csharp
string s1 = "Hello";

string s2 = s1;

s1 = s1 + " World";

Console.WriteLine(s1);
Console.WriteLine(s2);
```

Output

```text
Hello World
Hello
```

The original string remains unchanged.

---

# Declaring Strings

## Using String Literal

```csharp
string name = "John";
```

## Using String Constructor

```csharp
string name = new string("John".ToCharArray());
```

## Empty String

```csharp
string text = "";
```

or

```csharp
string text = String.Empty;
```

---

# Accessing Characters

```csharp
string text = "Hello";

Console.WriteLine(text[0]);
Console.WriteLine(text[4]);
```

Output

```text
H
o
```

---

# String Properties

| Property | Description |
|----------|-------------|
| Length | Returns number of characters |
| Chars[] | Returns character at index |

Example

```csharp
string text = "Programming";

Console.WriteLine(text.Length);
Console.WriteLine(text[3]);
```

---

# String Constructors

```text
String()

String(char[])

String(char, int)

String(char[], int startIndex, int length)
```

Example

```csharp
char[] letters = {'H','e','l','l','o'};

string word = new string(letters);

Console.WriteLine(word);
```

---

# Common String Methods

## Comparison

- Compare()
- CompareOrdinal()
- CompareTo()
- Equals()

---

## Searching

- Contains()
- StartsWith()
- EndsWith()
- IndexOf()
- LastIndexOf()
- IndexOfAny()
- LastIndexOfAny()

---

## Modification

- Replace()
- Remove()
- Insert()
- Trim()
- TrimStart()
- TrimEnd()
- PadLeft()
- PadRight()
- ToUpper()
- ToLower()
- ToUpperInvariant()
- ToLowerInvariant()

---

## Extraction

- Substring()
- Split()

---

## Conversion

- ToCharArray()
- ToString()
- Clone()
- CopyTo()

---

## Static Methods

- Join()
- Concat()
- Format()
- Copy()
- IsNullOrEmpty()
- IsNullOrWhiteSpace()
- Intern()
- IsInterned()

---

## Other Methods

- Normalize()
- GetHashCode()
- GetType()
- GetEnumerator()

---

# String Escape Sequences

| Escape | Meaning |
|---------|---------|
| `\n` | New Line |
| `\t` | Tab |
| `\\` | Backslash |
| `\"` | Double Quote |
| `\'` | Single Quote |
| `\r` | Carriage Return |
| `\b` | Backspace |
| `\a` | Alert |
| `\0` | Null Character |

Example

```csharp
Console.WriteLine("Hello\nWorld");
```

---

# Verbatim String

Prefix `@` ignores escape characters.

```csharp
string path = @"C:\Users\Deep\Desktop";

Console.WriteLine(path);
```

---

# Raw String Literal (C# 11)

Triple quotes allow writing multi-line strings without escaping.

```csharp
string json = """
{
    "Name":"John",
    "Age":20
}
""";
```

---

# String Interpolation

Uses `$` to insert variables into a string.

```csharp
string name = "John";
int age = 20;

Console.WriteLine($"Name : {name}");
Console.WriteLine($"Age : {age}");
```

---

# String Formatting

Uses placeholders.

```csharp
string name = "John";
int age = 20;

Console.WriteLine("{0} is {1} years old.", name, age);
```

---

# String Concatenation

Using `+`

```csharp
string first = "Hello";
string second = "World";

string result = first + " " + second;
```

Using `String.Concat()`

```csharp
string result = String.Concat(first, second);
```

Using `String.Join()`

```csharp
string result = String.Join("-", "A", "B", "C");
```

---

# StringBuilder

Namespace

```csharp
using System.Text;
```

---

# What is StringBuilder?

`StringBuilder` is a mutable sequence of characters.

Unlike `string`, the contents of a `StringBuilder` object can be modified **without creating a new object**.

It is mainly used when performing many string operations such as appending, inserting, deleting, or replacing text.

---

# Why use StringBuilder?

Suppose you append text 10,000 times.

Using `string`

```csharp
string text = "";

for(int i = 0; i < 10000; i++)
{
    text += i;
}
```

A **new string object** is created on every iteration.

---

Using `StringBuilder`

```csharp
StringBuilder sb = new StringBuilder();

for(int i = 0; i < 10000; i++)
{
    sb.Append(i);
}
```

The same object is modified repeatedly.

It is much faster and uses less memory.

---

# Creating a StringBuilder

```csharp
StringBuilder sb = new StringBuilder();
```

or

```csharp
StringBuilder sb = new StringBuilder("Hello");
```

---

# StringBuilder Properties

| Property | Description |
|----------|-------------|
| Length | Number of characters |
| Capacity | Allocated memory size |
| MaxCapacity | Maximum capacity |

---

# StringBuilder Methods

## Adding Text

- Append()
- AppendLine()
- AppendFormat()

---

## Modifying Text

- Insert()
- Remove()
- Replace()
- Clear()

---

## Capacity

- EnsureCapacity()

---

## Conversion

- ToString()
- CopyTo()

---

## Others

- Equals()

---

# StringBuilder Example

```csharp
using System;
using System.Text;

class Program
{
    static void Main()
    {
        StringBuilder sb = new StringBuilder();

        sb.Append("Hello");
        sb.Append(" ");
        sb.Append("World");

        Console.WriteLine(sb);

        sb.Replace("World", "C#");

        Console.WriteLine(sb);

        sb.Insert(6, "Programming ");

        Console.WriteLine(sb);

        sb.Remove(6, 12);

        Console.WriteLine(sb);
    }
}
```

Output

```text
Hello World
Hello C#
Hello Programming C#
Hello C#
```

---

# String vs StringBuilder

| String | StringBuilder |
|---------|---------------|
| Immutable | Mutable |
| Creates new object after modification | Modifies same object |
| Slower for repeated changes | Faster for repeated changes |
| Less memory efficient for updates | More memory efficient |
| Stored in `System.String` | Stored in `System.Text.StringBuilder` |
| Best for fixed text | Best for dynamic text |

---

# When to Use

### Use **String**

- Small text
- Constant values
- Read-only strings
- Few modifications

### Use **StringBuilder**

- Large text
- Loops
- File generation
- Log generation
- Repeated append, insert, replace, or remove operations