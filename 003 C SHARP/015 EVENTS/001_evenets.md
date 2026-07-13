# Events in C#

---

# What is an Event?

An **Event** is a notification mechanism used to inform one or more objects that something has happened.

Events are based on **delegates**.

Examples:

- Button Click
- Mouse Click
- Key Press
- File Download Completed
- User Login

---

# Why Use Events?

Events are used to:

- Notify other objects.
- Implement event-driven programming.
- Reduce coupling between classes.
- Support the Publisher-Subscriber pattern.

---

# Event Declaration

An event is declared using the `event` keyword.

### Syntax

```csharp
public event DelegateName EventName;
```

### Example

```csharp
using System;

delegate void Notify();

class Program
{
    public event Notify OnMessage;
}
```

---

# Event Handling

An event is handled by attaching (subscribing) a method to it.

### Example

```csharp
using System;

delegate void Notify();

class Publisher
{
    public event Notify OnMessage;

    public void SendMessage()
    {
        OnMessage?.Invoke();
    }
}

class Program
{
    static void ShowMessage()
    {
        Console.WriteLine("Event Received");
    }

    static void Main()
    {
        Publisher p = new Publisher();

        p.OnMessage += ShowMessage;

        p.SendMessage();
    }
}
```

**Output**

```text
Event Received
```

---

# Unsubscribing an Event

Use the `-=` operator to remove an event handler.

### Example

```csharp
Publisher p = new Publisher();

p.OnMessage += ShowMessage;

p.OnMessage -= ShowMessage;
```

---

# Publisher-Subscriber Pattern

The **Publisher-Subscriber Pattern** is a design pattern where:

- **Publisher** raises (fires) the event.
- **Subscriber** listens for the event and responds to it.

The publisher does not know who the subscribers are.

### Diagram

```text
        Event Raised
Publisher -----------> Subscriber 1
          |
          |---------> Subscriber 2
          |
          |---------> Subscriber 3
```

---

# Example

```csharp
using System;

delegate void Notify();

class Publisher
{
    public event Notify OnNotify;

    public void Start()
    {
        Console.WriteLine("Publisher Started");

        OnNotify?.Invoke();
    }
}

class Subscriber
{
    public void Receive()
    {
        Console.WriteLine("Subscriber Received Event");
    }
}

class Program
{
    static void Main()
    {
        Publisher publisher = new Publisher();

        Subscriber subscriber = new Subscriber();

        publisher.OnNotify += subscriber.Receive;

        publisher.Start();
    }
}
```

**Output**

```text
Publisher Started
Subscriber Received Event
```

---

# Event Keywords

| Keyword | Description |
|---------|-------------|
| `event` | Declares an event |
| `+=` | Subscribes to an event |
| `-=` | Unsubscribes from an event |
| `Invoke()` | Raises the event |
| `?.Invoke()` | Safely raises the event if subscribers exist |

---

# Advantages of Events

- Loose coupling between classes.
- Supports multiple subscribers.
- Easy communication between objects.
- Widely used in GUI applications.
- Foundation of event-driven programming.

---

# Difference Between Delegate and Event

| Delegate | Event |
|----------|-------|
| Can be invoked from anywhere it is accessible | Can only be raised by the declaring class |
| Used to reference methods | Used to notify subscribers |
| Does not provide access restriction | Provides controlled access using the `event` keyword |
