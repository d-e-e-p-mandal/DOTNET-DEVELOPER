# Operators in C#

---

# Operators

Operators are symbols used to perform operations on variables and values.

Example:

```csharp
int a = 10;
int b = 5;

int sum = a + b;
```

---

# Arithmetic Operators

Arithmetic operators are used to perform mathematical operations.

| Operator | Description | Example |
|----------|-------------|---------|
| `+` | Addition | `a + b` |
| `-` | Subtraction | `a - b` |
| `*` | Multiplication | `a * b` |
| `/` | Division | `a / b` |
| `%` | Modulus (Remainder) | `a % b` |

### Example

```csharp
int a = 10;
int b = 3;

Console.WriteLine(a + b);
Console.WriteLine(a - b);
Console.WriteLine(a * b);
Console.WriteLine(a / b);
Console.WriteLine(a % b);
```

---

# Relational Operators

Relational operators compare two values and return `true` or `false`.

| Operator | Description |
|----------|-------------|
| `==` | Equal to |
| `!=` | Not equal to |
| `>` | Greater than |
| `<` | Less than |
| `>=` | Greater than or equal to |
| `<=` | Less than or equal to |

### Example

```csharp
int a = 10;
int b = 20;

Console.WriteLine(a == b);
Console.WriteLine(a != b);
Console.WriteLine(a < b);
Console.WriteLine(a >= b);
```

---

# Logical Operators

Logical operators are used with boolean values.

| Operator | Description |
|----------|-------------|
| `&&` | Logical AND |
| `||` | Logical OR |
| `!` | Logical NOT |

### Example

```csharp
bool x = true;
bool y = false;

Console.WriteLine(x && y);
Console.WriteLine(x || y);
Console.WriteLine(!x);
```

---

# Assignment Operators

Assignment operators assign values to variables.

| Operator | Example |
|----------|---------|
| `=` | `a = 10` |
| `+=` | `a += 5` |
| `-=` | `a -= 5` |
| `*=` | `a *= 2` |
| `/=` | `a /= 2` |
| `%=` | `a %= 2` |

### Example

```csharp
int a = 10;

a += 5;
a *= 2;

Console.WriteLine(a);
```

---

# Unary Operators

Unary operators work on a single operand.

| Operator | Description |
|----------|-------------|
| `+` | Unary Plus |
| `-` | Unary Minus |
| `++` | Increment |
| `--` | Decrement |
| `!` | Logical NOT |

### Example

```csharp
int a = 5;

a++;
Console.WriteLine(a);

a--;
Console.WriteLine(a);
```

---

# Bitwise Operators

Bitwise operators perform operations on binary values.

| Operator | Description |
|----------|-------------|
| `&` | Bitwise AND |
| `|` | Bitwise OR |
| `^` | Bitwise XOR |
| `~` | Bitwise NOT |
| `<<` | Left Shift |
| `>>` | Right Shift |

### Example

```csharp
int a = 5;
int b = 3;

Console.WriteLine(a & b);
Console.WriteLine(a | b);
Console.WriteLine(a ^ b);
Console.WriteLine(a << 1);
Console.WriteLine(a >> 1);
```

---

# Ternary Operator

The ternary operator is a short form of the `if-else` statement.

### Syntax

```csharp
condition ? value1 : value2;
```

### Example

```csharp
int age = 20;

string result = (age >= 18) ? "Adult" : "Minor";

Console.WriteLine(result);
```
