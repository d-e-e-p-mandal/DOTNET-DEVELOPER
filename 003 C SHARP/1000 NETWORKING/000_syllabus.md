# .NET Networking — Complete Syllabus

## Module 1: Networking Fundamentals
- Client-Server Architecture
- Request-Response Model
- OSI Model & TCP/IP Model
- IP Address (IPv4/IPv6)
- Port Numbers
- URI / URL / URN
- DNS Basics
- Bandwidth, Latency, Throughput
- Unicast, Broadcast, Multicast, Anycast

## Module 2: Core Protocols
- TCP
- UDP
- HTTP / HTTPS
- HTTP/1.1, HTTP/2, HTTP/3, QUIC
- SSL/TLS
- WebSocket Protocol
- FTP / FTPS / SFTP
- SMTP / POP3 / IMAP
- SSH / Telnet
- MQTT / AMQP

## Module 3: HttpClient & Related Classes
- HttpClient
- HttpClientHandler
- IHttpClientFactory (Named, Typed, Generated Clients)
- DelegatingHandler
- HttpMessageHandler
- HttpRequestMessage
- HttpResponseMessage
- Connection Pooling
- Timeout & Retry Handling

## Module 4: HTTP Content Handling
- HttpContent
- StringContent
- ByteArrayContent
- StreamContent
- FormUrlEncodedContent
- MultipartFormDataContent (File Upload)

## Module 5: ASP.NET Core HTTP Pipeline
- HttpContext
- HttpRequest
- HttpResponse
- Middleware Pipeline
- IMiddleware
- RequestDelegate
- UseRouting, UseCors, UseAuthentication, UseAuthorization, UseStaticFiles, UseExceptionHandler

## Module 6: Web API Networking
- ControllerBase
- IActionResult / ActionResult<T>
- Routing (RouteAttribute, ApiControllerAttribute)
- Action Results (Ok, BadRequest, NotFound, Unauthorized, Created, NoContent)
- Model Binding from Request
- Swagger / OpenAPI

## Module 7: Authentication & Authorization
- IAuthenticationService (AuthenticateAsync, SignInAsync, SignOutAsync, ChallengeAsync)
- ClaimsPrincipal / ClaimsIdentity / Claim
- IAuthorizationService (AuthorizeAsync)
- AuthorizationPolicy
- JWT Authentication
- OAuth / OAuth2 / OpenID Connect
- API Key Authentication
- HMAC

## Module 8: Cookies & Sessions
- IRequestCookieCollection
- IResponseCookies (Append, Delete)
- ISession (Set, Get, Remove, Clear)
- Cache-Control Headers
- ETag

## Module 9: Serialization for Network Data
- JsonSerializer (Serialize, Deserialize)
- JsonDocument (Parse)
- JsonElement (GetProperty, GetString, GetInt32)
- XML Serialization (basic)

## Module 10: Real-Time Communication
- SignalR — Hub (OnConnectedAsync, OnDisconnectedAsync)
- IHubContext, HubCallerContext
- Groups & Clients Broadcasting
- WebSocket / ClientWebSocket (SendAsync, ReceiveAsync, CloseAsync)
- WebSocketManager
- Server-Sent Events (SSE)
- Long Polling

## Module 11: gRPC Networking
- GrpcChannel (ForAddress)
- ServerCallContext
- Protocol Buffers
- Unary Calls
- Client Streaming
- Server Streaming
- Bidirectional Streaming
- Deadlines & Metadata

## Module 12: Low-Level Socket Programming
- Socket Class
- SocketAsyncEventArgs
- Bind(), Listen(), Accept(), Connect(), Send(), Receive(), Close()
- Socket Options
- Socket Shutdown

## Module 13: TCP Programming
- TcpClient (Connect, GetStream, Close)
- TcpListener (Start, AcceptTcpClient, Stop)
- NetworkStream (Read, Write, Flush)
- Keep Alive
- Connection Timeout & Retry

## Module 14: UDP Programming
- UdpClient (Send, Receive, Close)
- Datagram Communication
- Broadcasting
- Multicasting

## Module 15: FTP / FTPS Programming
- FTP Connection & Authentication
- Upload / Download Files
- Rename / Delete Files
- Create / Delete Directory
- List Files
- Active Mode / Passive Mode
- FTPS — Explicit & Implicit
- Certificate Validation (FTPS)
- Secure Upload / Download

## Module 16: SFTP File Transfer

#### Renci.SshNet.SftpClient
- SSH/SFTP Connection Setup (via SSH.NET — `Renci.SshNet.SftpClient`)
- Username-Password Authentication
- Private Key / Public Key Authentication
- Host Key Verification
- Upload File / Download File
- Resume Upload / Resume Download
- List Files & Directories
- Create / Delete Directory
- Delete / Rename / Move / Copy File
- Change Directory
- Check File Exists / Directory Exists
- Read / Write / Append File Content
- File Permissions & Attributes
- Recursive Upload / Download (Folder)
- Connection Timeout & Reconnection
- Progress Reporting (Transfer %)
- Asynchronous & Background Transfer
- Logging & Error Handling (SFTP Exceptions)

#### WinSCP
- WinSCP Installation & Setup
- Session Configuration (`SessionOptions`)
- SFTP / SCP / FTP / FTPS / WebDAV / S3 Connection
- Username-Password Authentication
- Private Key / Public Key Authentication
- Pageant / SSH Agent Authentication
- Host Key Verification
- Open / Close / Reconnect Session
- Upload File / Download File
- Resume Upload / Resume Download
- Upload Multiple Files
- Download Multiple Files
- Synchronize Directories
- Mirror Directory
- List Files & Directories
- Search & Filter Files
- Create / Delete / Rename Directory
- Change Directory
- Delete / Rename / Move / Copy File
- Check File Exists / Directory Exists
- Read / Write / Append File Content
- File Permissions & Attributes
- Recursive Upload / Download (Folder)
- Symbolic Links
- Transfer Queue
- Progress Reporting (Transfer %)
- Speed Limiting
- Background & Parallel Transfer
- WinSCP .NET Assembly (`WinSCP.Session`)
- WinSCP Command Line (`winscp.com`)
- WinSCP Scripting
- PowerShell Automation
- Scheduled Automation
- Logging (Session / XML / Debug)
- Error Handling (WinSCP Exceptions)
- Connection Timeout & Retry Logic
- Security Best Practices
- Performance Optimization

## Module 17: Email Networking
- SmtpClient & SMTP Authentication
- HTML Email & Attachments
- POP3 Client
- IMAP Client
- Mail Message Parsing

## Module 18: DNS & IP Utilities
- Dns Class (GetHostName, GetHostAddresses, Resolve)
- IPAddress (Parse, TryParse)
- IPEndPoint
- Forward / Reverse DNS Lookup
- DNS Record Types (A, AAAA, CNAME, MX, TXT, PTR, SRV)

## Module 19: Network Security Classes
- SslStream (AuthenticateAsClient, AuthenticateAsServer)
- X509Certificate2
- Certificate Chain & Validation
- RandomNumberGenerator (GetBytes)
- CORS / CSRF / XSS Protection
- Rate Limiting

## Module 20: Compression for Network Data
- GZipStream (Read, Write)
- DeflateStream (Read, Write)
- Brotli Compression

## Module 21: Caching for Network/API Responses
- IMemoryCache (Get, Set, Remove)
- IDistributedCache (Get, Set, Remove)

## Module 22: Logging & Diagnostics
- ILogger (LogInformation, LogWarning, LogError, LogCritical, LogDebug)
- Request/Response Logging
- Ping & Traceroute (System.Net.NetworkInformation)
- NetworkInterface Info
- Connectivity Testing

## Module 23: Asynchronous Networking
- async/await in Networking Calls
- Task-based Network Operations
- CancellationToken
- Parallel & Concurrent Requests
- Streaming Responses

## Module 24: Error Handling in Networking
- HttpRequestException
- SocketException
- TimeoutException
- IOException
- Retry Policies
- Circuit Breaker Pattern
- Fallback Strategies

## Module 25: Proxy & Gateway Networking
- Forward Proxy / Reverse Proxy
- HTTP Proxy / SOCKS Proxy
- Proxy Authentication
- API Gateway
- Load Balancing
- HttpClientHandler Proxy Settings

## Module 26: Advanced & Distributed Networking
- Microservice Communication
- Service Discovery
- Health Checks
- Service Mesh
- Webhooks
- Named Pipes
- Inter-Process Communication (IPC)
- Unix Domain Sockets
- CDN Concepts

## Module 27: Cloud Networking (Optional / Applied)
- Azure Storage / Service Bus / Event Hub
- AWS S3 / SNS / SQS
- Google Cloud Storage
- RabbitMQ / Apache Kafka / MSMQ

---
