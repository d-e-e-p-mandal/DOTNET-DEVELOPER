# Variables & Data Types in C#

---

# Variables

A **variable** is a named memory location used to store data. Its value can be changed during program execution.

### Syntax

```csharp
dataType variableName = value;
```

### Example

```csharp
int age = 21;
string name = "John";

Console.WriteLine(age);
Console.WriteLine(name);
```

---

# Constants

A **constant** is a variable whose value cannot be changed after initialization.

Use the `const` keyword.

### Syntax

```csharp
const dataType name = value;
```

### Example

```csharp
const double PI = 3.14159;

Console.WriteLine(PI);
```

---

# Data Types

Data types define the type of data a variable can store.

## Common Data Types

| Data Type | Size | Example |
|-----------|------|---------|
| int | 4 Bytes | `int a = 10;` |
| long | 8 Bytes | `long n = 100000L;` |
| short | 2 Bytes | `short x = 20;` |
| byte | 1 Byte | `byte b = 255;` |
| float | 4 Bytes | `float f = 3.14f;` |
| double | 8 Bytes | `double d = 3.14159;` |
| decimal | 16 Bytes | `decimal price = 99.99m;` |
| char | 2 Bytes | `char ch = 'A';` |
| string | Variable | `string name = "Alice";` |
| bool | 1 Byte | `bool isActive = true;` |

---

## int

Stores whole numbers.

```csharp
int age = 25;
```

---

## long

Stores very large integers.

```csharp
long population = 8000000000L;
```

---

## short

Stores small integers.

```csharp
short marks = 95;
```

---

## byte

Stores values from **0 to 255**.

```csharp
byte number = 200;
```

---

## float

Stores single-precision decimal values.

```csharp
float height = 5.8f;
```

---

## double

Stores double-precision decimal values.

```csharp
double pi = 3.14159265;
```

---

## decimal

Used for financial and monetary calculations.

```csharp
decimal salary = 25000.75m;
```

---

## char

Stores a single character.

```csharp
char grade = 'A';
```

---

## string

Stores a sequence of characters.

```csharp
string message = "Hello C#";
```

---

## bool

Stores only two values.

```csharp
bool isLoggedIn = true;
```

---

# var Keyword

The `var` keyword lets the compiler determine the variable's type automatically.

### Example

```csharp
var age = 25;
var name = "John";
var price = 99.99;

Console.WriteLine(age);
Console.WriteLine(name);
```

**Note:** Once assigned, the type cannot change.

---

# dynamic Keyword

The `dynamic` keyword allows the type to be determined at runtime.

### Example

```csharp
dynamic value = 10;

Console.WriteLine(value);

value = "Hello";

Console.WriteLine(value);

value = true;

Console.WriteLine(value);
```

---

# Nullable Types

Normally, value types cannot store `null`.

Use `?` to make them nullable.

### Syntax

```csharp
dataType? variableName;
```

### Example

```csharp
int? age = null;

Console.WriteLine(age);

age = 25;

Console.WriteLine(age);
```

---

# Type Casting

Type casting converts one data type into another.

## Implicit Casting

Automatic conversion from a smaller type to a larger type.

```csharp
int num = 100;

double value = num;

Console.WriteLine(value);
```

---

## Explicit Casting

Manual conversion from a larger type to a smaller type.

```csharp
double price = 99.99;

int amount = (int)price;

Console.WriteLine(amount);
```

Output

```
99
```

---

# Boxing & Unboxing

## Boxing

Converting a **value type** into an **object**.

```csharp
int number = 100;

object obj = number;

Console.WriteLine(obj);
```

---

## Unboxing

Converting an **object** back to its original value type.

```csharp
object obj = 100;

int number = (int)obj;

Console.WriteLine(number);
```

---