# LINQ to XML in C# (.NET)

# Complete Guide (Reading & Writing XML)

---

# What is LINQ to XML?

LINQ to XML is a modern API introduced in .NET Framework 3.5 for creating, reading, searching, modifying, and deleting XML documents using LINQ (Language Integrated Query).

Instead of using older classes like:

- XmlDocument
- XmlNode
- XmlElement

LINQ to XML provides easier classes such as:

- XDocument
- XElement
- XAttribute
- XComment
- XDeclaration

which work naturally with LINQ queries.

---

# Namespace Required

```csharp
using System.Xml.Linq;
using System.Linq;
```

## System.Xml.Linq

Provides XML classes.

Examples

- XDocument
- XElement
- XAttribute
- XComment
- XCData
- XText
- XDeclaration

---

## System.Linq

Provides LINQ extension methods.

Examples

- Where()
- Select()
- First()
- FirstOrDefault()
- Single()
- Count()
- Any()
- OrderBy()
- GroupBy()
- ToList()

Without

```csharp
using System.Linq;
```

the compiler cannot recognize these methods because they are extension methods on `IEnumerable<T>`.

---

# LINQ to XML Object Model

```
XDocument
│
├── XDeclaration
│
├── XElement (Root)
│      │
│      ├── XElement
│      ├── XElement
│      ├── XElement
│      └── XElement
│
├── XComment
│
└── Processing Instruction
```

---

# Sample XML

```xml
<?xml version="1.0" encoding="utf-8"?>

<Employees>

    <Employee Id="1">

        <Name>Deep</Name>

        <Department>IT</Department>

        <Salary>50000</Salary>

    </Employee>

    <Employee Id="2">

        <Name>Rahul</Name>

        <Department>HR</Department>

        <Salary>40000</Salary>

    </Employee>

    <Employee Id="3">

        <Name>Amit</Name>

        <Department>IT</Department>

        <Salary>60000</Salary>

    </Employee>

</Employees>
```

---

# Loading XML

## Load from File

```csharp
XDocument doc =
XDocument.Load("Employees.xml");
```

---

## Load from String

```csharp
string xml = File.ReadAllText("Employees.xml");

XDocument doc =
XDocument.Parse(xml);
```

---

## Create Empty Document

```csharp
XDocument doc =
new XDocument();
```

---

# Saving XML

```csharp
doc.Save("Employees.xml");
```

---

# Important Classes

| Class | Purpose |
|--------|----------|
| XDocument | Entire XML document |
| XElement | XML element |
| XAttribute | XML attribute |
| XComment | XML comment |
| XCData | CDATA section |
| XDeclaration | XML declaration |
| XText | Text node |

---

# XML Navigation Methods

---

# Root

Returns root element.

```csharp
var root = doc.Root;
```

Output

```
Employees
```

---

# Descendants()

Returns every matching element recursively.

```csharp
var employees =
doc.Descendants("Employee");
```

Return Type

```csharp
IEnumerable<XElement>
```

Tree

```
Employees
│
├── Employee
│
├── Employee
│
└── Employee
```

Searches entire tree.

---

# Elements()

Returns only direct child elements.

```csharp
var employees =
doc.Root.Elements("Employee");
```

Only children of Root are returned.

---

# Element()

Returns first matching child.

```csharp
employee.Element("Name");
```

Returns

```csharp
XElement
```

---

# Attribute()

Returns attribute.

```csharp
employee.Attribute("Id");
```

Returns

```csharp
XAttribute
```

---

# Value

Returns element value.

```csharp
employee.Element("Name").Value;
```

Output

```
Deep
```

---

# Name

```csharp
employee.Name
```

Output

```
Employee
```

---

# HasElements

```csharp
employee.HasElements
```

Output

```
true
```

---

# HasAttributes

```csharp
employee.HasAttributes
```

Output

```
true
```

---

# Reading XML using LINQ

---

## Read Every Employee

```csharp
foreach(var employee in doc.Descendants("Employee"))
{
    Console.WriteLine(employee.Element("Name")?.Value);
}
```

Output

```
Deep
Rahul
Amit
```

---

# Read Attribute

```csharp
foreach(var employee in doc.Descendants("Employee"))
{
    Console.WriteLine(employee.Attribute("Id")?.Value);
}
```

Output

```
1
2
3
```

---

# Read Multiple Values

```csharp
foreach(var employee in doc.Descendants("Employee"))
{
    Console.WriteLine(

        employee.Attribute("Id")?.Value + " " +

        employee.Element("Name")?.Value + " " +

        employee.Element("Department")?.Value

    );
}
```

---

# LINQ Methods

---

# Where()

Filters data.

```csharp
var itEmployees =

doc.Descendants("Employee")

.Where(e =>

(string)e.Element("Department")=="IT");
```

Output

```
Deep
Amit
```

---

# Select()

Projects values.

```csharp
var names =

doc.Descendants("Employee")

.Select(e=>e.Element("Name")?.Value);
```

Output

```
Deep
Rahul
Amit
```

---

# First()

Returns first element.

Throws exception if collection is empty.

```csharp
var employee =

doc.Descendants("Employee")

.First();
```

---

# FirstOrDefault()

Returns first element.

Returns null if not found.

```csharp
var employee =

doc.Descendants("Employee")

.FirstOrDefault();
```

---

# Last()

Returns last element.

```csharp
var employee =

doc.Descendants("Employee")

.Last();
```

---

# LastOrDefault()

Returns last element or null.

```csharp
var employee =

doc.Descendants("Employee")

.LastOrDefault();
```

---

# Single()

Exactly one item must exist.

Throws exception when

- zero found
- more than one found

```csharp
var employee =

doc.Descendants("Employee")

.Single(e=>

(string)e.Attribute("Id")=="1");
```

---

# SingleOrDefault()

Returns one item.

Returns null when none exists.

Throws exception when multiple exist.

```csharp
var employee =

doc.Descendants("Employee")

.SingleOrDefault(e=>

(string)e.Attribute("Id")=="1");
```

---

# Any()

Checks existence.

```csharp
bool exists =

doc.Descendants("Employee")

.Any(e=>

(string)e.Element("Department")=="IT");
```

Output

```
true
```

---

# All()

Checks every element.

```csharp
bool allIT =

doc.Descendants("Employee")

.All(e=>

(string)e.Element("Department")=="IT");
```

---

# Count()

Counts items.

```csharp
int total =

doc.Descendants("Employee")

.Count();
```

---

# Sum()

```csharp
int totalSalary =

doc.Descendants("Employee")

.Sum(e=>

(int)e.Element("Salary"));
```

---

# Average()

```csharp
double avg =

doc.Descendants("Employee")

.Average(e=>

(int)e.Element("Salary"));
```

---

# Min()

```csharp
int min =

doc.Descendants("Employee")

.Min(e=>

(int)e.Element("Salary"));
```

---

# Max()

```csharp
int max =

doc.Descendants("Employee")

.Max(e=>

(int)e.Element("Salary"));
```

---

# OrderBy()

Ascending sort.

```csharp
var employees =

doc.Descendants("Employee")

.OrderBy(e=>

(string)e.Element("Name"));
```

---

# OrderByDescending()

Descending sort.

```csharp
var employees =

doc.Descendants("Employee")

.OrderByDescending(e=>

(int)e.Element("Salary"));
```

---

# ThenBy()

Secondary sorting.

```csharp
.OrderBy(e=>e.Element("Department").Value)

.ThenBy(e=>e.Element("Name").Value)
```

---

# GroupBy()

```csharp
var groups =

doc.Descendants("Employee")

.GroupBy(e=>

(string)e.Element("Department"));
```

---

# Skip()

```csharp
.Skip(2)
```

Skips first two records.

---

# Take()

```csharp
.Take(5)
```

Returns first five records.

---

# SkipWhile()

Skips until condition becomes false.

---

# TakeWhile()

Takes while condition is true.

---

# Distinct()

Removes duplicates.

---

# Reverse()

Reverse order.

---

# Contains()

Checks value exists.

---

# ToList()

Converts IEnumerable to List.

```csharp
List<XElement> employees =

doc.Descendants("Employee")

.ToList();
```

Why?

- Store in memory
- Access by index
- Multiple iterations
- Better performance when reused

---

# ToArray()

```csharp
XElement[] employees =

doc.Descendants("Employee")

.ToArray();
```

---

# Deferred Execution

LINQ queries are lazy.

```csharp
var query =

doc.Descendants("Employee")

.Where(e=>

(string)e.Element("Department")=="IT");
```

Nothing executes yet.

Execution occurs here

```csharp
foreach(var e in query)
{
}
```

or

```csharp
query.ToList();
```

---

# Writing XML

---

# Create XML

```csharp
XDocument doc =

new XDocument(

new XElement("Employees")

);
```

---

# Add Employee

```csharp
doc.Root.Add(

new XElement("Employee",

new XAttribute("Id",1),

new XElement("Name","Deep"),

new XElement("Department","IT"),

new XElement("Salary",50000)

)

);
```

Output

```xml
<Employees>

    <Employee Id="1">

        <Name>Deep</Name>

        <Department>IT</Department>

        <Salary>50000</Salary>

    </Employee>

</Employees>
```

---

# Add Multiple Employees

```csharp
doc.Root.Add(

new XElement("Employee",
new XAttribute("Id",2),
new XElement("Name","Rahul"),
new XElement("Department","HR"),
new XElement("Salary",40000)
),

new XElement("Employee",
new XAttribute("Id",3),
new XElement("Name","Amit"),
new XElement("Department","IT"),
new XElement("Salary",60000)
)

);
```

---

# Update Value

```csharp
var employee =

doc.Descendants("Employee")

.First();

employee.Element("Salary").Value="70000";
```

---

# Update Attribute

```csharp
employee.Attribute("Id").Value="10";
```

---

# Add New Element

```csharp
employee.Add(

new XElement("City","Kolkata")

);
```

---

# Add New Attribute

```csharp
employee.Add(

new XAttribute("Age",25)

);
```

---

# Remove Element

```csharp
employee.Element("City").Remove();
```

---

# Remove Attribute

```csharp
employee.Attribute("Age").Remove();
```

---

# Remove Entire Employee

```csharp
employee.Remove();
```

---

# Replace Element

```csharp
employee.ReplaceWith(

new XElement("Employee",

new XAttribute("Id",100),

new XElement("Name","New Employee")

)

);
```

---

# Replace Child Element

```csharp
employee.Element("Name")

.ReplaceWith(

new XElement("Name","Deep Mandal")

);
```

---

# Add Before

```csharp
employee.AddBeforeSelf(

new XElement("Employee")

);
```

---

# Add After

```csharp
employee.AddAfterSelf(

new XElement("Employee")

);
```

---

# Comments

```csharp
doc.Root.Add(

new XComment("Employee List")

);
```

---

# CDATA

```csharp
new XCData("<b>Hello</b>")
```

Output

```xml
<![CDATA[<b>Hello</b>]]>
```

---

# XML Declaration

```csharp
new XDeclaration(

"1.0",

"utf-8",

"yes"

);
```

---

# Save XML

```csharp
doc.Save("Employees.xml");
```

---

# Method Chaining Example

```csharp
var result =

doc.Descendants("Employee")

.Where(e=>

(string)e.Element("Department")=="IT")

.OrderByDescending(e=>

(int)e.Element("Salary"))

.Select(e=>new
{
    Id=(string)e.Attribute("Id"),
    Name=(string)e.Element("Name"),
    Salary=(int)e.Element("Salary")
})

.ToList();
```

---

# IEnumerable vs List

| IEnumerable | List |
|--------------|------|
| Lazy execution | Immediate execution |
| Read-only enumeration | Collection in memory |
| Less memory | More memory |
| Best for queries | Best for repeated access |

---

# LINQ Query Syntax

Method Syntax

```csharp
var employees =

doc.Descendants("Employee")

.Where(e=>

(string)e.Element("Department")=="IT");
```

Query Syntax

```csharp
var employees =

from e in doc.Descendants("Employee")

where (string)e.Element("Department")=="IT"

select e;
```

---

# Exception Safety

Instead of

```csharp
employee.Element("Name").Value
```

Prefer

```csharp
employee.Element("Name")?.Value
```

Avoids

```
NullReferenceException
```

---

# Async Support

LINQ to XML itself does **not** provide asynchronous query methods such as:

- `FirstOrDefaultAsync()`
- `SingleAsync()`
- `ToListAsync()`
- `CountAsync()`

These methods belong to **Entity Framework Core** (`Microsoft.EntityFrameworkCore`) and are used with databases, not XML.

XML operations are typically synchronous:

```csharp
XDocument.Load("Employees.xml");
```

```csharp
doc.Save("Employees.xml");
```

Some lower-level APIs (such as `XmlReader`/`XmlWriter`) support asynchronous operations, but standard LINQ to XML querying and manipulation does not include async LINQ methods.

---

# Quick Summary

| Method | Read | Write | Purpose |
|---------|------|-------|---------|
| Load() | ✔ | | Load XML |
| Parse() | ✔ | | Load XML from string |
| Save() | | ✔ | Save XML |
| Root | ✔ | ✔ | Root element |
| Descendants() | ✔ | ✔ | All matching elements recursively |
| Elements() | ✔ | ✔ | Direct child elements |
| Element() | ✔ | ✔ | First child element |
| Attribute() | ✔ | ✔ | Access an attribute |
| Value | ✔ | ✔ | Get or set element value |
| Add() | | ✔ | Add element or attribute |
| Remove() | | ✔ | Remove node or attribute |
| ReplaceWith() | | ✔ | Replace node |
| AddBeforeSelf() | | ✔ | Insert before current node |
| AddAfterSelf() | | ✔ | Insert after current node |
| Where() | ✔ | | Filter records |
| Select() | ✔ | | Project values |
| First() | ✔ | | First element |
| FirstOrDefault() | ✔ | | First element or null |
| Last() | ✔ | | Last element |
| LastOrDefault() | ✔ | | Last element or null |
| Single() | ✔ | | Exactly one element |
| SingleOrDefault() | ✔ | | One element or null |
| Any() | ✔ | | Check existence |
| All() | ✔ | | Check all satisfy condition |
| Count() | ✔ | | Count elements |
| Sum() | ✔ | | Total numeric values |
| Average() | ✔ | | Average numeric values |
| Min() | ✔ | | Minimum value |
| Max() | ✔ | | Maximum value |
| OrderBy() | ✔ | | Sort ascending |
| OrderByDescending() | ✔ | | Sort descending |
| ThenBy() | ✔ | | Secondary sort |
| GroupBy() | ✔ | | Group data |
| Skip() | ✔ | | Skip records |
| Take() | ✔ | | Take records |
| Distinct() | ✔ | | Remove duplicates |
| Reverse() | ✔ | | Reverse sequence |
| ToList() | ✔ | | Convert to `List<XElement>` |
| ToArray() | ✔ | | Convert to `XElement[]` |

---

# Best Practices

- Always use `?.Value` when an element may not exist.
- Prefer `FirstOrDefault()` over `First()` unless you are certain data exists.
- Use `Single()` only when exactly one matching element is expected.
- Use `ToList()` if you'll enumerate the results multiple times.
- Keep XML queries readable by chaining LINQ methods clearly.
- Save changes with `doc.Save()` after modifying the XML.
- Cast element values directly when appropriate, e.g. `(int)e.Element("Salary")`.
- Use `Descendants()` for recursive searches and `Elements()` for direct children only.
```





-----------------


LINQ to XML is used for both reading and writing XML.

Operation	Supported by LINQ to XML?	Examples
Read XML	✅ Yes	Load, Search, Filter, Select
Create XML	✅ Yes	new XDocument(), new XElement()
Add Elements	✅ Yes	Add()
Update Elements	✅ Yes	Value = ..., SetValue()
Update Attributes	✅ Yes	Attribute().Value = ..., SetAttributeValue()
Delete Elements	✅ Yes	Remove()
Delete Attributes	✅ Yes	Remove()
Replace Elements	✅ Yes	ReplaceWith()
Save XML	✅ Yes	Save()

1. Reading XML

XDocument doc = XDocument.Load("Employees.xml");
var employees = doc.Descendants("Employee")
                   .Where(e => (string)e.Element("Department") == "IT")
                   .ToList();

This reads and filters XML data.

⸻

2. Writing XML

Create XML

XDocument doc = new XDocument(
    new XElement("Employees")
);

⸻

Add Data

doc.Root.Add(
    new XElement("Employee",
        new XAttribute("Id", "1"),
        new XElement("Name", "Deep"),
        new XElement("Department", "IT")
    )
);

⸻

Update Data

var employee = doc.Descendants("Employee").First();
employee.Element("Name").Value = "Deep Mandal";

⸻

Delete Data

doc.Descendants("Employee").First().Remove();

⸻

Save XML

doc.Save("Employees.xml");

⸻

Does LINQ itself write XML?

This is an important distinction:

* LINQ methods (Where(), Select(), FirstOrDefault(), OrderBy(), etc.) are primarily for querying (reading/filtering/projecting) collections.
* LINQ to XML classes (XDocument, XElement, XAttribute) provide the ability to create, add, update, remove, and save XML.

So when people say “LINQ to XML”, they mean the combination of:

* LINQ → used to query and find XML nodes.
* LINQ to XML API → used to create and modify the XML document.

In short

* LINQ = Query language (mainly reading/filtering/projection).
* LINQ to XML = Read ✅ + Create ✅ + Update ✅ + Delete ✅ + Save ✅ XML.

So LINQ to XML is not read-only—it supports full CRUD (Create, Read, Update, Delete) operations on XML.