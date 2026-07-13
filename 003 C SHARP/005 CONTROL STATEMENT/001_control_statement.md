# Control Statements in C#

---

# Control Statements

Control statements are used to control the flow of program execution.

They help make decisions, repeat tasks, or jump to another part of the program.

---

# if Statement

The `if` statement executes a block of code only if the condition is `true`.

### Syntax

```csharp
if (condition)
{
    // Code
}
```

### Example

```csharp
int age = 20;

if (age >= 18)
{
    Console.WriteLine("Eligible to Vote");
}
```

---

# if-else Statement

The `if-else` statement executes one block if the condition is true, otherwise another block.

### Syntax

```csharp
if (condition)
{
    // True block
}
else
{
    // False block
}
```

### Example

```csharp
int age = 16;

if (age >= 18)
{
    Console.WriteLine("Adult");
}
else
{
    Console.WriteLine("Minor");
}
```

---

# Nested if

A nested `if` means an `if` statement inside another `if`.

### Example

```csharp
int age = 20;
bool hasLicense = true;

if (age >= 18)
{
    if (hasLicense)
    {
        Console.WriteLine("Can Drive");
    }
}
```

---

# switch Statement

The `switch` statement selects one block of code from multiple options.

### Syntax

```csharp
switch (expression)
{
    case value:
        // Code
        break;

    default:
        // Default Code
        break;
}
```

### Example

```csharp
int day = 2;

switch (day)
{
    case 1:
        Console.WriteLine("Monday");
        break;

    case 2:
        Console.WriteLine("Tuesday");
        break;

    default:
        Console.WriteLine("Invalid Day");
        break;
}
```

---

# switch Expressions

A switch expression returns a value using a simpler syntax.

### Example

```csharp
int day = 1;

string result = day switch
{
    1 => "Monday",
    2 => "Tuesday",
    3 => "Wednesday",
    _ => "Invalid"
};

Console.WriteLine(result);
```

---

# for Loop

The `for` loop is used when the number of iterations is known.

### Syntax

```csharp
for(initialization; condition; update)
{
    // Code
}
```

### Example

```csharp
for (int i = 1; i <= 5; i++)
{
    Console.WriteLine(i);
}
```

---

# while Loop

The `while` loop executes as long as the condition is true.

### Syntax

```csharp
while(condition)
{
    // Code
}
```

### Example

```csharp
int i = 1;

while (i <= 5)
{
    Console.WriteLine(i);
    i++;
}
```

---

# do-while Loop

The `do-while` loop executes the block at least once.

### Syntax

```csharp
do
{
    // Code
}
while(condition);
```

### Example

```csharp
int i = 1;

do
{
    Console.WriteLine(i);
    i++;
}
while (i <= 5);
```

---

# foreach Loop

The `foreach` loop is used to iterate through arrays and collections.

### Syntax

```csharp
foreach(dataType item in collection)
{
    // Code
}
```

### Example

```csharp
string[] names = { "John", "Alice", "Bob" };

foreach (string name in names)
{
    Console.WriteLine(name);
}
```

---

# break Statement

The `break` statement immediately exits a loop or switch.

### Example

```csharp
for (int i = 1; i <= 10; i++)
{
    if (i == 5)
        break;

    Console.WriteLine(i);
}
```

**Output**

```text
1
2
3
4
```

---

# continue Statement

The `continue` statement skips the current iteration and moves to the next iteration.

### Example

```csharp
for (int i = 1; i <= 5; i++)
{
    if (i == 3)
        continue;

    Console.WriteLine(i);
}
```

**Output**

```text
1
2
4
5
```

---

# goto Statement

The `goto` statement transfers control to a labeled statement.

> **Note:** It is rarely used because it can make code difficult to read.

### Example

```csharp
int number = 2;

switch (number)
{
    case 1:
        Console.WriteLine("One");
        break;

    case 2:
        goto case 1;

    default:
        Console.WriteLine("Other");
        break;
}
```

---

# return Statement

The `return` statement exits a method and optionally returns a value.

### Example

```csharp
static int Add(int a, int b)
{
    return a + b;
}

Console.WriteLine(Add(10, 20));
```