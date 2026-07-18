# XmlNode.AppendChild() in .NET

## Definition

`AppendChild()` adds an existing or newly created node as the **last child** of another node.

**Syntax**

```csharp
parentNode.AppendChild(childNode);
```

- **Parent Node** → The node on which `AppendChild()` is called.
- **Child Node** → The node that will be added.
- The child is always inserted as the **last child**.
- It returns the appended node.
- If the child already belongs to another parent, it is **removed from the old parent and moved** to the new parent.
- A node cannot have two parents at the same time.

---

# Example 1 - Create Root

## Step 1

Create an empty document.

```csharp
XmlDocument doc = new XmlDocument();
```

Tree

```text
Document
```

XML

```xml
(empty)
```

---

## Step 2

Create the root element.

```csharp
XmlElement employees = doc.CreateElement("Employees");
```

Tree

```text
Document

Employees (Not attached yet)
```

XML

```xml
(empty)
```

Nothing changes because the node is only created.

---

## Step 3

Attach the root to the document.

```csharp
doc.AppendChild(employees);
```

Tree

```text
Document
│
└── Employees
```

XML

```xml
<Employees>
</Employees>
```

---

# Example 2 - Create First Employee

## Step 1

Create Employee.

```csharp
XmlElement employee = doc.CreateElement("Employee");
```

Tree

```text
Document
│
└── Employees

Employee (Not attached yet)
```

---

## Step 2

Append Employee.

```csharp
employees.AppendChild(employee);
```

Tree

```text
Document
│
└── Employees
      │
      └── Employee
```

XML

```xml
<Employees>
    <Employee>
    </Employee>
</Employees>
```

---

# Example 3 - Create Name

## Step 1

Create Name node.

```csharp
XmlElement name = doc.CreateElement("Name");
```

Tree

```text
Document
│
└── Employees
      │
      └── Employee

Name (Not attached yet)
```

---

## Step 2

Append Name to Employee.

```csharp
employee.AppendChild(name);
```

Tree

```text
Document
│
└── Employees
      │
      └── Employee
             │
             └── Name
```

XML

```xml
<Employees>
    <Employee>
        <Name>
        </Name>
    </Employee>
</Employees>
```

---

# Example 4 - Add Text

```csharp
name.InnerText = "John";
```

Tree

```text
Document
│
└── Employees
      │
      └── Employee
             │
             └── Name
                    │
                    └── "John"
```

XML

```xml
<Employees>
    <Employee>
        <Name>John</Name>
    </Employee>
</Employees>
```

---

# Example 5 - Department

```csharp
XmlElement department = doc.CreateElement("Department");
department.InnerText = "IT";

employee.AppendChild(department);
```

Tree

```text
Document
│
└── Employees
      │
      └── Employee
             │
             ├── Name
             │     │
             │     └── "John"
             │
             └── Department
                   │
                   └── "IT"
```

XML

```xml
<Employees>
    <Employee>
        <Name>John</Name>
        <Department>IT</Department>
    </Employee>
</Employees>
```

---

# Example 6 - Salary

```csharp
XmlElement salary = doc.CreateElement("Salary");
salary.InnerText = "50000";

employee.AppendChild(salary);
```

Tree

```text
Document
│
└── Employees
      │
      └── Employee
             │
             ├── Name
             │
             ├── Department
             │
             └── Salary
```

XML

```xml
<Employees>
    <Employee>
        <Name>John</Name>
        <Department>IT</Department>
        <Salary>50000</Salary>
    </Employee>
</Employees>
```

---

# Example 7 - Second Employee

```csharp
XmlElement employee2 = doc.CreateElement("Employee");

employees.AppendChild(employee2);
```

Tree

```text
Document
│
└── Employees
      │
      ├── Employee
      │
      └── Employee
```

XML

```xml
<Employees>
    <Employee>
        <Name>John</Name>
        <Department>IT</Department>
        <Salary>50000</Salary>
    </Employee>

    <Employee>
    </Employee>
</Employees>
```

---

# Example 8 - Append Nested Child

```csharp
XmlElement address = doc.CreateElement("Address");
employee.AppendChild(address);
```

Tree

```text
Document
│
└── Employees
      │
      ├── Employee
      │      │
      │      ├── Name
      │      ├── Department
      │      ├── Salary
      │      └── Address
      │
      └── Employee
```

XML

```xml
<Employees>
    <Employee>
        <Name>John</Name>
        <Department>IT</Department>
        <Salary>50000</Salary>
        <Address>
        </Address>
    </Employee>

    <Employee>
    </Employee>
</Employees>
```

---

# Example 9 - Append Child Inside Child

```csharp
XmlElement city = doc.CreateElement("City");

address.AppendChild(city);

city.InnerText = "Kolkata";
```

Tree

```text
Document
│
└── Employees
      │
      ├── Employee
      │      │
      │      ├── Name
      │      ├── Department
      │      ├── Salary
      │      └── Address
      │             │
      │             └── City
      │                    │
      │                    └── "Kolkata"
      │
      └── Employee
```

XML

```xml
<Employees>
    <Employee>
        <Name>John</Name>
        <Department>IT</Department>
        <Salary>50000</Salary>

        <Address>
            <City>Kolkata</City>
        </Address>

    </Employee>

    <Employee>
    </Employee>
</Employees>
```

---

# Example 10 - Append Existing Node (Move)

Suppose Employee 1 contains Address.

```text
Employees
│
├── Employee1
│      │
│      └── Address
│
└── Employee2
```

Now execute

```csharp
employee2.AppendChild(address);
```

Address is **not copied**.

It is **removed** from Employee1 and **moved** to Employee2.

Tree

```text
Employees
│
├── Employee1
│
└── Employee2
       │
       └── Address
```

XML

```xml
<Employees>

    <Employee>
        <Name>John</Name>
        <Department>IT</Department>
        <Salary>50000</Salary>
    </Employee>

    <Employee>

        <Address>
            <City>Kolkata</City>
        </Address>

    </Employee>

</Employees>
```

---

# Important Rules

- Adds the node as the **last child**.
- Parent must already exist.
- Child can be newly created or an existing node.
- Existing nodes are **moved**, not copied.
- Returns the appended node.
- Parent can contain many child nodes.
- Child can also contain its own children.
- Root node is attached using `doc.AppendChild(root)`.
- Nested XML is created by repeatedly calling `AppendChild()`.
- One node cannot belong to multiple parents simultaneously.