
# XML APIs in .NET

.NET provides four major APIs.

| API | Purpose |
|------|----------|
| XmlDocument | Read, Edit and Save XML |
| XmlReader | Read XML efficiently |
| XmlWriter | Create XML |
| LINQ to XML | Modern XML Programming |

---

# 2. XmlDocument

- `XmlDocument` is a DOM (Document Object Model) parser.
- It loads the **entire XML document into memory**.

**Once loaded, you can:**
- Read
- Search
- Update
- Delete
- Insert
- Save

> It is best suited for **small and medium XML files**.

---

## Internal Working
```
Employees
│
├── Employee
│      │
│      ├── Name
│      ├── Department
│      └── Salary
│
└── Employee
       │
       ├── Name
       ├── Department
       └── Salary
```

- Everything is loaded into RAM.
- That's why navigation is very easy.

---

## Namespace

```csharp
using System.Xml;
```

---

## Create Object
```csharp
XmlDocument doc = new XmlDocument();
```

## Load XML
- Loads XML from a file.
```csharp
doc.Load("Employees.xml");
```


## Load XML String
- Loads XML from a string.

```csharp
string xml = "<Employee><Name>Deep</Name></Employee>";
doc.LoadXml(xml);
```



---

## Save XML

```csharp
doc.Save("Employees.xml");
```
- Writes changes back to the file.

---

# Reading XML

## SelectSingleNode()
- Returns only one node.
- Only first matching node.
- Use when `only one node is expected.`
```csharp
XmlNode node =
doc.SelectSingleNode("/Employees/Employee/Name");

Console.WriteLine(node.InnerText);
```

**Output:** `Deep Mandal`


---

## SelectNodes()
- Returns multiple nodes.
- All matching nodes.
- Use when multiple matching nodes exist.

```csharp
XmlNodeList employees = doc.SelectNodes("/Employees/Employee");

foreach(XmlNode emp in employees)
{
    Console.WriteLine(emp["Name"].InnerText);
}
```

**Output:**
- Deep Mandal 
- Rahul

---

## CreateElement()
- Creates a new XML element.

```csharp
XmlElement employee = doc.CreateElement("Employee");
```

## Set Value
```csharp
employee.InnerText="New Employee";
```

---

## AppendChild()
- Adds a child node.

```csharp
doc.DocumentElement.AppendChild(employee);
```

Now the XML becomes

```xml
<Employee>

New Employee

</Employee>
```

---

## RemoveChild()
- Removes a node.

```csharp
doc.DocumentElement.RemoveChild(employee);
```

---

## CreateAttribute()

Creates a new attribute.

```csharp
XmlAttribute id =
doc.CreateAttribute("Id");

id.Value="103";
```

Attach it

```csharp
employee.Attributes.Append(id);
```

Output

```xml
<Employee Id="103">
```

---

## Common Properties

| Property | Description |
|----------|-------------|
| InnerText | Gets or sets text |
| InnerXml | Gets XML inside node |
| OuterXml | Gets complete XML |
| Name | Node name |
| Value | Node value |
| Attributes | Node attributes |
| ChildNodes | Child collection |
| ParentNode | Parent |

---

## Advantages

- Easy to use
- XPath support
- Supports CRUD
- Random access
- Rich API

---

## Disadvantages

- High memory usage
- Slow for huge XML files
- Loads entire document

---

## When to Use XmlDocument

Use XmlDocument when:

- XML size is small or medium
- You need to modify XML
- You need XPath queries
- You need CRUD operations
- Random navigation is required

---
