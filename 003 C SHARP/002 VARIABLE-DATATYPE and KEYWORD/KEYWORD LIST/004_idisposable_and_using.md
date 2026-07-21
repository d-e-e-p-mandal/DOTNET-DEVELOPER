# using keyword in c# for exception:
- this (using) is used only if IDisposable Interface implements

## IDisposable Interface in C#

**Definition :**  IDisposable is an interface in C# used to Release resources manually using the Dispose() method

Syntax
```cs
public interface IDisposable
{
    void Dispose();
}
```

⸻

Why we need it?

Some resources are not handled automatically by memory (Garbage Collector), like:
	•	Database connections
	•	Files
	•	Network resources

So we use: Dispose() → to free resources manually


Custom Class Example
```cs
using System;

public class MyResource : IDisposable
{
    public void Open()
    {
        Console.WriteLine("Resource opened");
    }

    public void Dispose()
    {
        Console.WriteLine("Resource cleaned (Dispose called)");
    }
}
```


Key Points :
✅ Must implement Dispose()
✅ Used for cleanup
✅ Required for using keyword


## using Keyword in C#

Definition : using is a C# keyword used to Automatically call Dispose() after using an object

Why use using?

- Without using 
```cs
var obj = new MyResource();
obj.Open();
// may forget
obj.Dispose();
```

- With using 
```cs
using (var obj = new MyResource())
{
    obj.Open();
}
```

**Internal Working**

Compiler converts:
```cs
using (var obj = new MyResource())
{
    obj.Open();
}
```
-> Into:
```cs
var obj = new MyResource();
try
{
    obj.Open();
}
finally
{
    obj.Dispose(); // always runs
}
```

⸻

using var (Modern C#)
```cs
using var obj = new MyResource();

obj.Open();

Dispose() is called at end of scope
```
⸻

Example with Exception
```cs
using (var obj = new MyResource())
{
    obj.Open();
    throw new Exception("Error"); 
}
```
Output:
- Resource opened
- Resource cleaned (Dispose called)

Even after error → cleanup happens ✅

⸻

**Important Rules**
using works only if class implements: IDisposable

Otherwise: Error
```cs
using (var obj = new MyClass()) // ❌ ERROR
```
------

📘 Predefined Classes that Implement IDisposable


1️⃣ Database Related

Used in ADO.NET / EF Core
	•	DbContext
	•	SqlConnection
	•	SqlCommand
	•	SqlDataReader
	•	SqlTransaction

From:
	•	System.Data.SqlClient
	•	Microsoft.EntityFrameworkCore

⸻

2️⃣ File & Stream Classes

Used for file handling
	•	FileStream
	•	StreamReader
	•	StreamWriter
	•	BinaryReader
	•	BinaryWriter
	•	MemoryStream

From:
	•	System.IO

⸻

3️⃣ Network & IO
	•	TcpClient
	•	TcpListener
	•	NetworkStream
	•	HttpClient

From:
	•	System.Net
	•	System.Net.Http

⸻

4️⃣ Graphics / Drawing
	•	Bitmap
	•	Image
	•	Graphics
	•	Font
	•	Pen
	•	Brush

From:
	•	System.Drawing

⸻

5️⃣ Threading / Timers
	•	Timer
	•	CancellationTokenSource

From:
	•	System.Threading

⸻

6️⃣ Security / Cryptography
	•	Aes
	•	RSA
	•	HashAlgorithm
	•	CryptoStream

From:
	•	System.Security.Cryptography

⸻

7️⃣ ASP.NET Core / Web
	•	HttpContext (indirectly)
	•	IServiceScope
	•	DbContext

From:
	•	ASP.NET Core

⸻

8️⃣ Others (Common)
	•	Process
	•	Mutex
	•	Semaphore
	•	RegistryKey


**Why all these implement IDisposable?**

Because they use:

External resources (not managed by Garbage Collector)

Like:
	•	File handles
	•	DB connections
	•	Network sockets

⸻

**`Unmanaged resource → implements IDisposable`**

- IDisposable = used by classes that need manual cleanup

- Many .NET predefined classes like DbContext, FileStream, SqlConnection, and HttpClient implement IDisposable because they manage unmanaged resources that require explicit cleanup.
