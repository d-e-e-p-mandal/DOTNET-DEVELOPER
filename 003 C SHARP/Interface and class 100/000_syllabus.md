# .NET / C# IMPORTANT FRAMEWORK CLASSES, INTERFACES & METHODS

## Hosting

### IHost
- StartAsync()
- StopAsync()
- Run()
- Dispose()

### IHostBuilder
- ConfigureServices()
- ConfigureAppConfiguration()
- ConfigureLogging()
- Build()

### WebApplication
- Run()
- MapGet()
- MapPost()
- MapPut()
- MapDelete()
- UseMiddleware()
- UseAuthentication()
- UseAuthorization()


---

## Dependency Injection

### IServiceCollection
- AddSingleton()
- AddScoped()
- AddTransient()
- BuildServiceProvider()

### IServiceProvider
- GetService()
- GetRequiredService()
- CreateScope()

### IServiceScopeFactory
- CreateScope()

---

## Configuration

### IConfiguration
- GetSection()
- GetValue()

### IConfigurationSection
- Get()
- Exists()

---

## Logging

### ILogger
- LogInformation()
- LogWarning()
- LogError()
- LogCritical()
- LogDebug()
- LogTrace()

### ILoggerFactory
- CreateLogger()

---

## HTTP Client

### HttpClient
- GetAsync()
- PostAsync()
- PutAsync()
- DeleteAsync()
- PatchAsync()
- SendAsync()

### IHttpClientFactory
- CreateClient()

### HttpRequestMessage
- Headers
- Content
- Method
- RequestUri

### HttpResponseMessage
- EnsureSuccessStatusCode()
- StatusCode
- Content

### HttpContent
- ReadAsStringAsync()
- ReadAsByteArrayAsync()
- ReadAsStreamAsync()

### StringContent

### MultipartFormDataContent
- Add()

### HttpClientHandler

### DelegatingHandler
- SendAsync()

---

## ASP.NET Core Request Context

### HttpContext
- Request
- Response
- User
- Session
- Connection

### HttpRequest
- Headers
- Query
- Form
- Cookies
- Body

### HttpResponse
- StatusCode
- Headers
- Cookies
- Redirect()

---

## Controllers

### ControllerBase
- Ok()
- BadRequest()
- NotFound()
- Unauthorized()
- Created()
- File()

### Controller
- View()
- Redirect()
- RedirectToAction()

### IActionResult

### ActionResult<T>

---

## Middleware

### IMiddleware
- InvokeAsync()

### RequestDelegate
- Invoke()

---

## Authentication

### IAuthenticationService
- AuthenticateAsync()
- ChallengeAsync()
- SignInAsync()
- SignOutAsync()

### ClaimsPrincipal

### ClaimsIdentity

### Claim

---

## Authorization

### IAuthorizationService
- AuthorizeAsync()

### AuthorizationPolicy

---

## Session & Cookies

### ISession
- Set()
- SetString()
- Get()
- GetString()
- Remove()
- Clear()

### IRequestCookieCollection

### IResponseCookies
- Append()
- Delete()

---

## File Handling

### File
- Create()
- ReadAllText()
- ReadAllLines()
- WriteAllText()
- WriteAllLines()
- AppendAllText()
- Copy()
- Move()
- Delete()
- Exists()

### FileInfo
- Create()
- CopyTo()
- MoveTo()
- Delete()

### Directory
- CreateDirectory()
- Delete()
- Move()
- Exists()
- GetFiles()
- GetDirectories()

### DirectoryInfo
- Create()
- Delete()
- GetFiles()
- GetDirectories()

### Path
- Combine()
- GetFileName()
- GetExtension()
- GetDirectoryName()
- GetFullPath()

---

## Streams

### Stream
- Read()
- Write()
- Flush()
- Seek()
- Close()

### FileStream
- Read()
- Write()
- Flush()

### StreamReader
- Read()
- ReadLine()
- ReadToEnd()

### StreamWriter
- Write()
- WriteLine()
- Flush()

### BinaryReader
- ReadString()
- ReadInt32()
- ReadBytes()

### BinaryWriter
- Write()

### MemoryStream

---

## JSON

### JsonSerializer
- Serialize()
- Deserialize()

### JsonDocument
- Parse()

### JsonElement
- GetString()
- GetInt32()
- GetProperty()

---

## XML

### XmlDocument
- Load()
- Save()

### XmlReader
- Read()

### XmlWriter
- WriteStartElement()
- WriteEndElement()

### XmlSerializer
- Serialize()
- Deserialize()

---

## Entity Framework Core

### DbContext
- SaveChanges()
- SaveChangesAsync()
- Add()
- Update()
- Remove()
- Find()

### DbSet<T>
- Add()
- AddRange()
- Update()
- Remove()
- Find()
- ToList()
- FirstOrDefault()

### ModelBuilder
- Entity()
- HasKey()

---

## LINQ

### Enumerable

#### Filtering
- Where()

#### Projection
- Select()
- SelectMany()

#### Sorting
- OrderBy()
- OrderByDescending()
- ThenBy()

#### Grouping
- GroupBy()

#### Joining
- Join()
- GroupJoin()

#### Aggregation
- Count()
- Sum()
- Min()
- Max()
- Average()

#### Element
- First()
- FirstOrDefault()
- Single()
- SingleOrDefault()
- Last()

#### Quantifiers
- Any()
- All()

#### Set
- Distinct()
- Union()
- Intersect()
- Except()

#### Conversion
- ToList()
- ToArray()
- ToDictionary()

---

## Collections

### List<T>
- Add()
- AddRange()
- Remove()
- RemoveAt()
- Clear()
- Contains()
- Find()

### Dictionary<TKey,TValue>
- Add()
- Remove()
- ContainsKey()
- TryGetValue()

### HashSet<T>
- Add()
- Remove()
- Contains()

### Queue<T>
- Enqueue()
- Dequeue()
- Peek()

### Stack<T>
- Push()
- Pop()
- Peek()

---

## Tasks & Async

### Task
- Run()
- Wait()
- Delay()
- WhenAll()
- WhenAny()

### Task<T>

### CancellationToken
- Cancel()
- ThrowIfCancellationRequested()

---

## SignalR

### Hub
- OnConnectedAsync()
- OnDisconnectedAsync()

### IHubContext
- Clients
- Groups

### HubCallerContext

---

## gRPC

### ServerCallContext

### GrpcChannel
- ForAddress()

---

## Validation

### ValidationAttribute
- IsValid()

### RequiredAttribute

### StringLengthAttribute

### RangeAttribute

---

## Security

### PasswordHasher<TUser>
- HashPassword()
- VerifyHashedPassword()

### RandomNumberGenerator
- GetBytes()

---

## Caching

### IMemoryCache
- Get()
- Set()
- Remove()

### IDistributedCache
- Get()
- Set()
- Remove()

---

## Serialization

### BinaryFormatter
- Serialize()
- Deserialize()

### DataContractSerializer
- WriteObject()
- ReadObject()

---

## Networking

### TcpClient
- Connect()
- GetStream()

### TcpListener
- Start()
- AcceptTcpClient()
- Stop()

### UdpClient
- Send()
- Receive()

### Socket
- Connect()
- Bind()
- Listen()
- Accept()
- Send()
- Receive()

---

## Reflection

### Type
- GetProperties()
- GetMethods()
- GetFields()

### PropertyInfo
- GetValue()
- SetValue()

### MethodInfo
- Invoke()

---

## Threading

### Thread
- Start()
- Sleep()
- Join()

### Monitor
- Enter()
- Exit()

### Mutex
- WaitOne()
- ReleaseMutex()

### Semaphore
- WaitOne()
- Release()

### ReaderWriterLockSlim
- EnterReadLock()
- ExitReadLock()
- EnterWriteLock()
- ExitWriteLock()