# 16. XML File Handling

## What is XML?

**XML (eXtensible Markup Language)** is a text-based markup language used to **store, organize, and exchange structured data** between different applications and platforms.

Unlike HTML, XML does not have predefined tags. You can create your own tags according to your application's requirements.

### Features

- Human-readable
- Machine-readable
- Platform-independent
- Language-independent
- Hierarchical structure
- Self-descriptive
- Easy to transfer over a network

---

## Why XML is Used?

XML is commonly used for:

- Configuration files (`app.config`, `web.config`)
- Data storage
- Data exchange between applications
- SOAP Web Services
- Import/Export data
- API responses
- Application settings

---

## XML Structure

An XML document consists of:

- **Declaration** – Defines XML version and encoding.
- **Root Element** – The top-level element.
- **Child Elements** – Nested elements inside the root.
- **Attributes** – Additional information about an element.
- **Text Content** – Actual data stored in elements.

### Example XML

```xml
<?xml version="1.0" encoding="UTF-8"?>

<Employees>

    <Employee Id="101">
        <Name>Deep Mandal</Name>
        <Department>IT</Department>
        <Salary>50000</Salary>
    </Employee>

    <Employee Id="102">
        <Name>Rahul</Name>
        <Department>HR</Department>
        <Salary>45000</Salary>
    </Employee>

</Employees>
```

---

# XML APIs in .NET

.NET provides multiple APIs to work with XML.

| API | Purpose |
|------|----------|
| XmlDocument | Read, edit, and save XML |
| XmlReader | Fast forward-only reading |
| XmlWriter | Create XML documents |
| LINQ to XML | Modern XML manipulation |

---

# 1. XmlDocument

## What is XmlDocument?

`XmlDocument` is based on the **Document Object Model (DOM)**.

It loads the **entire XML document into memory**, allowing you to move freely through the document, update nodes, delete nodes, or add new elements.

### Internal Working

```
Employees
│
├── Employee
│     ├── Name
│     ├── Department
│     └── Salary
│
└── Employee
      ├── Name
      ├── Department
      └── Salary
```

The complete XML file is stored as a tree structure in memory.

---

## Namespace

```csharp
using System.Xml;
```

---

## When to Use

Use `XmlDocument` when you need to:

- Read XML
- Modify XML
- Delete elements
- Add elements
- Save changes

---

## Load XML File

```csharp
using System.Xml;

XmlDocument doc = new XmlDocument();
doc.Load("Employees.xml");
```

---

## Read a Single Node

```csharp
XmlNode node = doc.SelectSingleNode("/Employees/Employee/Name");

Console.WriteLine(node.InnerText);
```

### Output

```
Deep Mandal
```

---

## Read Multiple Employees

```csharp
XmlNodeList employees = doc.SelectNodes("/Employees/Employee");

foreach (XmlNode emp in employees)
{
    Console.WriteLine(emp["Name"].InnerText);
}
```

### Output

```
Deep Mandal
Rahul
```

---

## Create a New Element

```csharp
XmlElement employee = doc.CreateElement("Employee");

employee.InnerText = "New Employee";
```

---

## Add Element

```csharp
doc.DocumentElement.AppendChild(employee);
```

---

## Save XML

```csharp
doc.Save("Employees.xml");
```

---

## Common Methods

| Method | Description |
|---------|-------------|
| Load() | Loads an XML file |
| LoadXml() | Loads XML from a string |
| Save() | Saves XML |
| SelectSingleNode() | Returns one node |
| SelectNodes() | Returns multiple nodes |
| CreateElement() | Creates an element |
| CreateAttribute() | Creates an attribute |
| AppendChild() | Adds a child node |
| RemoveChild() | Removes a child node |

---

## Advantages

- Easy to understand
- Supports editing
- Supports XPath
- Rich API

---

## Disadvantages

- High memory usage
- Slow for very large XML files

---

# 2. XmlReader

## What is XmlReader?

`XmlReader` is a **forward-only, read-only** XML parser.

Instead of loading the entire XML into memory, it reads one node at a time.

### Internal Working

```
Employee 1
      ↓
Employee 2
      ↓
Employee 3
      ↓
End of File
```

Once a node has been read, you cannot move backward.

---

## Namespace

```csharp
using System.Xml;
```

---

## When to Use

Use `XmlReader` when:

- Reading large XML files
- High performance is required
- Low memory usage is important
- You only need to read data

---

## Read XML

```csharp
using System.Xml;

using XmlReader reader = XmlReader.Create("Employees.xml");

while (reader.Read())
{
    if (reader.NodeType == XmlNodeType.Element &&
        reader.Name == "Name")
    {
        Console.WriteLine(reader.ReadElementContentAsString());
    }
}
```

### Output

```
Deep Mandal
Rahul
```

---

## Common Methods

| Method | Description |
|---------|-------------|
| Read() | Reads the next node |
| MoveToContent() | Moves to content |
| ReadElementContentAsString() | Reads text |
| ReadElementContentAsInt() | Reads integer |
| GetAttribute() | Reads attribute value |
| Close() | Closes the reader |

---

## Advantages

- Very fast
- Uses very little memory
- Best for huge XML files

---

## Disadvantages

- Cannot modify XML
- Forward-only
- Read-only

---

# 3. XmlWriter

## What is XmlWriter?

`XmlWriter` is used to **create XML documents**.

It writes XML directly to a file or stream without storing the entire document in memory.

---

## Namespace

```csharp
using System.Xml;
```

---

## When to Use

Use `XmlWriter` when:

- Creating a new XML document
- Exporting data
- Writing configuration files

---

## Create XML

```csharp
using System.Xml;

using XmlWriter writer = XmlWriter.Create("Employees.xml");

writer.WriteStartDocument();

writer.WriteStartElement("Employees");

writer.WriteStartElement("Employee");

writer.WriteElementString("Name", "Deep Mandal");
writer.WriteElementString("Department", "IT");

writer.WriteEndElement();

writer.WriteEndElement();

writer.WriteEndDocument();

writer.Close();
```

### Generated XML

```xml
<?xml version="1.0"?>

<Employees>
    <Employee>
        <Name>Deep Mandal</Name>
        <Department>IT</Department>
    </Employee>
</Employees>
```

---

## Common Methods

| Method | Description |
|---------|-------------|
| WriteStartDocument() | Starts XML document |
| WriteStartElement() | Starts an element |
| WriteElementString() | Writes an element with text |
| WriteAttributeString() | Writes an attribute |
| WriteString() | Writes text |
| WriteEndElement() | Ends an element |
| WriteEndDocument() | Ends XML document |
| Flush() | Writes remaining data |
| Close() | Closes the writer |

---

## Advantages

- Fast
- Memory efficient
- Produces valid XML

---

## Disadvantages

- Cannot read XML
- Cannot edit existing XML

---

# 4. LINQ to XML

## What is LINQ to XML?

LINQ to XML is the **modern XML API** introduced in .NET.

It uses classes like:

- XDocument
- XElement
- XAttribute

It provides a clean and readable syntax and supports LINQ queries for searching and filtering XML data.

---

## Namespace

```csharp
using System.Xml.Linq;
```

---

## When to Use

Use LINQ to XML when:

- Creating XML
- Reading XML
- Updating XML
- Searching XML using LINQ
- Developing modern .NET applications

---

## Create XML

```csharp
using System.Xml.Linq;

XDocument doc = new XDocument(

    new XElement("Employees",

        new XElement("Employee",

            new XElement("Name", "Deep Mandal"),
            new XElement("Department", "IT")
        )
    )
);

doc.Save("Employees.xml");
```

---

## Read XML

```csharp
XDocument doc = XDocument.Load("Employees.xml");

foreach (var emp in doc.Descendants("Employee"))
{
    Console.WriteLine(emp.Element("Name").Value);
}
```

### Output

```
Deep Mandal
```

---

## Add a New Employee

```csharp
doc.Root.Add(

    new XElement("Employee",

        new XElement("Name", "Rahul"),
        new XElement("Department", "HR")
    )
);

doc.Save("Employees.xml");
```

---

## Common Methods

| Method | Description |
|---------|-------------|
| Load() | Loads XML |
| Save() | Saves XML |
| Parse() | Reads XML from string |
| Descendants() | Gets all descendants |
| Elements() | Gets child elements |
| Element() | Gets a single child element |
| Attribute() | Gets an attribute |
| Add() | Adds an element |
| Remove() | Removes an element |

---

## Advantages

- Clean syntax
- Easy to learn
- Supports LINQ queries
- Easy searching
- Easy filtering
- Easy updating

---

## Disadvantages

- Loads XML into memory
- Not suitable for extremely large XML files

---

# Comparison

| Feature | XmlDocument | XmlReader | XmlWriter | LINQ to XML |
|----------|-------------|-----------|------------|--------------|
| Read XML | ✅ | ✅ | ❌ | ✅ |
| Write XML | ✅ | ❌ | ✅ | ✅ |
| Modify XML | ✅ | ❌ | ❌ | ✅ |
| Memory Usage | High | Very Low | Very Low | Medium |
| Performance | Medium | Very High | Very High | High |
| Easy to Learn | Medium | Medium | Easy | Very Easy |
| Best For | Editing XML | Large XML Reading | Creating XML | Modern XML Development |

---

# Which One Should You Use?

| Requirement | Recommended API |
|-------------|-----------------|
| Read a small XML file | LINQ to XML |
| Edit an existing XML file | XmlDocument |
| Read a very large XML file | XmlReader |
| Create a new XML document | XmlWriter |
| Modern .NET applications | LINQ to XML |

---

# Summary

- **XmlDocument** loads the entire XML document into memory and is best for editing existing XML files.
- **XmlReader** reads XML sequentially with very low memory usage, making it ideal for large XML files.
- **XmlWriter** efficiently creates and writes well-formed XML documents.
- **LINQ to XML** provides a modern, simple, and powerful way to create, query, and modify XML using LINQ syntax.