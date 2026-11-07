🟦 GROUP 03 — .NET PLATFORM & RUNTIME
│
├── 10. .NET PLATFORM
│   │
│   ├── 10.01 INTRODUCTION TO THE .NET PLATFORM
│   │   ├── What Is .NET?
│   │   ├── Programming Languages, Compilers, Runtimes, and Libraries
│   │   ├── C# Language versus .NET Platform
│   │   ├── Application Code versus Framework Code
│   │   ├── Managed Execution and Runtime Services
│   │   └── Console, Web, Desktop, Mobile, Cloud, and Library Applications
│   │
│   ├── 10.02 .NET FRAMEWORK, .NET CORE, AND MODERN .NET
│   │   ├── .NET Framework and Its Windows-Based Application Models
│   │   ├── .NET Core and Cross-Platform Development
│   │   ├── Modern Unified .NET
│   │   ├── Shared Concepts and Important Implementation Differences
│   │   ├── Framework Libraries versus Application Frameworks
│   │   └── Compatibility and Migration Boundaries
│   │
│   ├── 10.03 PLATFORM COMPONENTS
│   │   ├── .NET SDK
│   │   ├── .NET Runtime
│   │   ├── ASP.NET Core Shared Framework
│   │   ├── Windows Desktop Shared Framework
│   │   ├── Compilers and Build Tools
│   │   ├── Reference Assemblies and Runtime Assemblies
│   │   └── Targeting Packs, Runtime Packs, and Workloads
│   │
│   ├── 10.04 LANGUAGE INTEROPERABILITY
│   │   ├── Common Language Infrastructure: CLI
│   │   ├── Common Type System: CTS
│   │   ├── Common Language Specification: CLS
│   │   ├── Common Intermediate Language: CIL
│   │   ├── C#, F#, and Visual Basic
│   │   ├── Sharing Libraries across .NET Languages
│   │   └── CLS-Compliant Public APIs and Language-Specific Features
│   │
│   ├── 10.05 .NET STANDARD
│   │   ├── .NET Standard as an API Specification
│   │   ├── API Contracts versus Runtime Implementations
│   │   ├── .NET Standard Versions and Implementation Support
│   │   ├── Library Compatibility across .NET Implementations
│   │   ├── .NET Standard versus Targeting Modern .NET Directly
│   │   └── Choosing Targets for New and Existing Libraries
│   │
│   ├── 10.06 TARGET FRAMEWORKS AND COMPATIBILITY
│   │   ├── Target Framework Monikers: TFMs
│   │   ├── Platform-Specific Target Frameworks
│   │   ├── Single-Targeting and Multi-Targeting
│   │   ├── Compile-Time API Availability
│   │   ├── Package Compatibility and Asset Selection
│   │   ├── Source, Binary, and Behavioral Compatibility
│   │   └── Language Version versus SDK Version versus Runtime Version
│   │
│   ├── 10.07 CROSS-PLATFORM ARCHITECTURE
│   │   ├── Operating System and Processor Architecture
│   │   ├── Windows, Linux, and macOS Support Boundaries
│   │   ├── x64, ARM64, and Other Supported Targets
│   │   ├── Portable Managed Code and Platform-Specific Native Code
│   │   ├── Runtime Identifier: RID
│   │   ├── File Paths, Permissions, Case Sensitivity, and Line Endings
│   │   ├── Globalization, Time Zones, and Native Dependencies
│   │   └── Platform Guards and Compatibility Analyzers
│   │
│   ├── 10.08 RUNTIME IMPLEMENTATIONS AND EXECUTION ENVIRONMENTS
│   │   ├── CoreCLR and Mono Overview
│   │   ├── JIT, Interpreter, and AOT Execution Models
│   │   ├── Desktop and Server Execution Environments
│   │   ├── Browser and WebAssembly Environments
│   │   ├── Mobile Runtime and Deployment Constraints
│   │   └── Runtime Capabilities versus Application Framework Support
│   │
│   └── 10.09 VERSIONING AND PLATFORM LIFECYCLE
│       ├── Runtime Versions and SDK Versions
│       ├── Major, Minor, and Servicing Releases
│       ├── LTS and STS Support Policies
│       ├── Side-by-Side Installation
│       ├── Supported Operating Systems and Architectures
│       ├── Breaking Changes and Compatibility Testing
│       └── Upgrade Planning and Runtime Servicing Responsibility
│
├── 11. CLR
│   │
│   ├── 11.01 CLR RESPONSIBILITIES
│   │   ├── What Is the Common Language Runtime?
│   │   ├── Loading and Executing Managed Applications
│   │   ├── Type Loading and Runtime Type Information
│   │   ├── Memory Management
│   │   ├── Exception Processing
│   │   ├── Threading and Synchronization Services
│   │   └── Native Interoperability and Diagnostic Services
│   │
│   ├── 11.02 MANAGED AND UNMANAGED EXECUTION
│   │   ├── Managed Code and Runtime Participation
│   │   ├── Unmanaged Code and Native Libraries
│   │   ├── Managed Objects versus Unmanaged Resources
│   │   ├── Transitions between Managed and Native Code
│   │   ├── Type Safety and Memory Safety
│   │   ├── Unsafe Code within a Managed Application
│   │   └── Why Managed Execution Is Not a Security Sandbox
│   │
│   ├── 11.03 APPLICATION EXECUTION LIFECYCLE
│   │   ├── Runtime Initialization
│   │   ├── Loading the Entry Assembly
│   │   ├── Resolving Types and Dependencies
│   │   ├── Static Initialization and Type Initializers
│   │   ├── Entering Application Code
│   │   ├── Executing Methods and Runtime Services
│   │   └── Normal Exit, Unhandled Failure, and Process Termination
│   │
│   ├── 11.04 JUST-IN-TIME COMPILATION
│   │   ├── Why IL Needs an Execution Strategy
│   │   ├── Compiling Methods into Native Instructions
│   │   ├── First-Call Compilation and Reusing Generated Code
│   │   ├── Processor-Specific Code Generation
│   │   ├── Debug versus Release Compilation Considerations
│   │   ├── Startup Cost versus Steady-State Performance
│   │   └── JIT Execution versus Precompiled Deployment
│   │
│   ├── 11.05 RUNTIME OPTIMIZATION
│   │   ├── Tiered Compilation
│   │   ├── Dynamic Profile-Guided Optimization
│   │   ├── On-Stack Replacement Concepts
│   │   ├── Method Inlining
│   │   ├── Devirtualization
│   │   ├── Bounds-Check Elimination and Other Optimizations
│   │   └── Optimization Variability across Versions and Workloads
│   │
│   ├── 11.06 TYPE EXECUTION AND METHOD DISPATCH
│   │   ├── Runtime Type Identity
│   │   ├── Instance, Static, Virtual, and Interface Calls
│   │   ├── Virtual Dispatch and Interface Dispatch
│   │   ├── Generic Type and Method Instantiation
│   │   ├── Generic Code Sharing and Specialization Concepts
│   │   ├── Boxing, Unboxing, and Runtime Cast Checks
│   │   └── Type Initialization Failures
│   │
│   ├── 11.07 RUNTIME EXCEPTION PROCESSING
│   │   ├── Managed Exception Objects
│   │   ├── Finding a Matching Handler
│   │   ├── Exception Filters and Handler Selection
│   │   ├── Stack Unwinding
│   │   ├── finally Execution and Cleanup Boundaries
│   │   ├── Stack Traces and Preserving Exception Information
│   │   ├── Unhandled Exceptions and Process Behavior
│   │   └── Application Exception Patterns → Exception Handling Group
│   │
│   ├── 11.08 RUNTIME THREADING SERVICES
│   │   ├── Managed Threads and Operating-System Threads
│   │   ├── Thread Pool Responsibilities
│   │   ├── Runtime Scheduling versus Task Scheduling
│   │   ├── ExecutionContext and Ambient State
│   │   ├── Synchronization Primitives and Runtime Support
│   │   ├── Cooperation between Threads and Garbage Collection
│   │   └── Detailed Task and Thread Programming → Concurrency Group
│   │
│   └── 11.09 RUNTIME SERVICES AND THEIR LIMITS
│       ├── Automatic Memory Management → Chapter 12
│       ├── Assembly Resolution and Loading → Chapter 13
│       ├── Native Interoperability Boundaries
│       ├── Debugger, Profiler, and Event Instrumentation Hooks
│       ├── Runtime Configuration and Feature Availability
│       └── Separating Compiler Behavior from Runtime Behavior
│
├── 12. RUNTIME MEMORY
│   │
│   ├── 12.01 PROCESS MEMORY FOUNDATIONS
│   │   ├── Virtual Address Space
│   │   ├── Reserved, Committed, and Resident Memory
│   │   ├── Thread Stacks, Managed Heaps, and Native Allocations
│   │   ├── Code, Metadata, and Memory-Mapped Regions
│   │   ├── Process Memory versus Managed Heap Size
│   │   └── Operating-System and Container Memory Limits
│   │
│   ├── 12.02 STACKS AND EXECUTION FRAMES
│   │   ├── Per-Thread Stacks
│   │   ├── Method Calls and Stack Frames
│   │   ├── Parameters, Local Storage, and Return Information
│   │   ├── Registers and Compiler Optimization
│   │   ├── Recursion and Stack Exhaustion
│   │   └── Why Source-Level Locals Do Not Map to Fixed Storage Rules
│   │
│   ├── 12.03 OBJECTS, VALUES, AND STORAGE
│   │   ├── Object References and Object Data
│   │   ├── Value Types Embedded in Objects and Arrays
│   │   ├── Object Headers, Fields, Alignment, and Padding Concepts
│   │   ├── Boxing Allocations
│   │   ├── Arrays, Strings, and Their Storage Characteristics
│   │   ├── Static Fields and Captured Variables
│   │   └── Implementation Details versus Language Guarantees
│   │
│   ├── 12.04 MANAGED HEAP ORGANIZATION
│   │   ├── Small Object Heap: SOH
│   │   ├── Large Object Heap: LOH
│   │   ├── Pinned Object Heap: POH
│   │   ├── Heap Segments and Regions
│   │   ├── Allocation Contexts and Allocation Paths
│   │   ├── Fragmentation and Free Space
│   │   └── Heap Categories versus Garbage-Collection Generations
│   │
│   ├── 12.05 REACHABILITY AND OBJECT LIFETIME
│   │   ├── GC Roots
│   │   ├── References from Stacks, Statics, Handles, and Runtime Structures
│   │   ├── Object Graph Traversal
│   │   ├── Reachable versus Unreachable Objects
│   │   ├── Cyclic References
│   │   ├── Lexical Scope versus GC-Observed Lifetime
│   │   └── Retention through Events, Closures, Caches, and Static State
│   │
│   ├── 12.06 GENERATIONAL GARBAGE COLLECTION
│   │   ├── Generation 0, Generation 1, and Generation 2
│   │   ├── The Generational Hypothesis
│   │   ├── Object Survival and Promotion
│   │   ├── Ephemeral Collections and Full Collections
│   │   ├── Allocation Pressure and Collection Triggers
│   │   ├── LOH and POH Collection Relationships
│   │   └── Generation Number versus Actual Object Age
│   │
│   ├── 12.07 COLLECTION MECHANICS
│   │   ├── Suspending and Coordinating Managed Execution
│   │   ├── Marking Reachable Objects
│   │   ├── Reclaiming Unreachable Storage
│   │   ├── Relocation and Compaction
│   │   ├── Updating Managed References
│   │   ├── Write Barriers and Remembered References
│   │   └── Pause Duration versus Total Collection Work
│   │
│   ├── 12.08 GC MODES AND CONFIGURATION
│   │   ├── Workstation GC and Server GC
│   │   ├── Background and Blocking Collections
│   │   ├── GC Latency Modes
│   │   ├── Heap Limits and Memory-Constrained Environments
│   │   ├── Explicit GC.Collect and Its Tradeoffs
│   │   ├── No-GC Regions and Their Constraints
│   │   └── Choosing Settings from Measurements
│   │
│   ├── 12.09 FINALIZATION
│   │   ├── Finalizable Objects and Runtime Registration
│   │   ├── Finalization Queues and Finalizer Execution
│   │   ├── Nondeterministic Timing and Ordering
│   │   ├── Finalization and Object Survival
│   │   ├── GC.SuppressFinalize
│   │   ├── Resurrection and Re-Registration Concepts
│   │   └── Why Finalizers Cannot Guarantee Application-Level Completion
│   │
│   ├── 12.10 DISPOSAL AND UNMANAGED RESOURCES
│   │   ├── Memory Reclamation versus Resource Release
│   │   ├── Owned versus Borrowed Resources
│   │   ├── IDisposable and IAsyncDisposable Lifecycle
│   │   ├── SafeHandle and Native Handle Ownership
│   │   ├── GC.KeepAlive and Lifetime Boundaries
│   │   ├── Unmanaged Memory Pressure
│   │   └── Full Dispose Patterns → Resource Management Group
│   │
│   ├── 12.11 PINNING AND WEAK REFERENCES
│   │   ├── Movable Objects and Native Pointer Stability
│   │   ├── fixed, GCHandle, and Pinning Lifetimes
│   │   ├── Pinning Costs and Fragmentation
│   │   ├── Pinned Allocations versus Pinning Existing Objects
│   │   ├── WeakReference and WeakReference<T>
│   │   ├── ConditionalWeakTable
│   │   └── Weak References versus Correct Cache Ownership
│   │
│   └── 12.12 ALLOCATION AND MEMORY INVESTIGATION
│       ├── Allocation Rate versus Retained Memory
│       ├── Temporary Objects, Boxing, Closures, and Iterator Allocations
│       ├── ArrayPool<T>, Object Pooling, and Retention Tradeoffs
│       ├── Span<T> and Memory<T> as Views Rather Than Automatic Ownership
│       ├── Managed Retention versus Native Leaks
│       ├── OutOfMemoryException and Memory Exhaustion Scenarios
│       ├── Inspecting GC Counters, Traces, and Dumps
│       └── Detailed Investigation Tools → Diagnostics Group
│
├── 13. IL & ASSEMBLIES
│   │
│   ├── 13.01 THE COMPILATION PIPELINE
│   │   ├── Source Files and Compiler Inputs
│   │   ├── Parsing, Binding, and Semantic Analysis
│   │   ├── Lowering High-Level Language Constructs
│   │   ├── Emitting CIL and Metadata
│   │   ├── Producing Assemblies and Debugging Symbols
│   │   └── Runtime Execution of the Compiled Result
│   │
│   ├── 13.02 CIL, IL, AND MSIL
│   │   ├── Terminology and Historical Naming
│   │   ├── Intermediate Instructions versus CPU Instructions
│   │   ├── Stack-Based Evaluation Model
│   │   ├── Arguments, Locals, and Constants
│   │   ├── Arithmetic, Comparisons, and Branches
│   │   ├── Method Calls, Object Creation, and Return Instructions
│   │   └── Exception-Handling Regions in Method Bodies
│   │
│   ├── 13.03 READING GENERATED IL
│   │   ├── Disassemblers and Decompilers
│   │   ├── Mapping Simple C# Expressions to IL
│   │   ├── Inspecting Fields, Properties, and Method Calls
│   │   ├── Boxing and Unboxing Instructions
│   │   ├── Compiler-Generated Closures and State Machines
│   │   ├── Debug versus Release Output
│   │   └── Decompilation Limits and Lost Source Information
│   │
│   ├── 13.04 ASSEMBLY STRUCTURE
│   │   ├── Assemblies as Deployment and Identity Units
│   │   ├── Managed Modules
│   │   ├── Portable Executable File Structure Overview
│   │   ├── Assembly Manifest
│   │   ├── Metadata Tables and Method Bodies
│   │   ├── Embedded and Linked Resources
│   │   └── Logical Assembly Structure versus File Extension
│   │
│   ├── 13.05 METADATA AND TYPE DESCRIPTION
│   │   ├── Type Definitions and Type References
│   │   ├── Method, Field, Property, and Event Metadata
│   │   ├── Signatures and Generic Parameters
│   │   ├── Assembly References
│   │   ├── Custom Attributes
│   │   ├── Metadata Tokens
│   │   └── Runtime Type Information versus Source-Level Syntax
│   │
│   ├── 13.06 DLL, EXE, AND PDB FILES
│   │   ├── Managed Class Libraries
│   │   ├── Managed Application Assemblies
│   │   ├── Native Apphost Executables
│   │   ├── Native Libraries versus Managed DLLs
│   │   ├── Portable PDBs and Source Mapping
│   │   ├── Embedded Symbols and Source Link
│   │   └── Debugging with Matching Binaries and Symbols
│   │
│   ├── 13.07 ASSEMBLY IDENTITY AND VERSIONING
│   │   ├── Assembly Name, Version, Culture, and Public Key Information
│   │   ├── AssemblyVersion, FileVersion, and InformationalVersion
│   │   ├── Assembly Version versus NuGet Package Version
│   │   ├── Strong Names and Signing
│   │   ├── Strong-Name Identity versus Publisher Trust
│   │   ├── Public API Compatibility
│   │   └── Type Forwarding and Version Evolution
│   │
│   ├── 13.08 DEPENDENCY RESOLUTION AND LOADING
│   │   ├── Compile-Time References versus Runtime Dependencies
│   │   ├── Default AssemblyLoadContext
│   │   ├── Managed and Native Dependency Resolution
│   │   ├── Dependency Conflicts and Missing Assemblies
│   │   ├── Assembly Identity and Type Identity across Load Contexts
│   │   ├── Collectible Contexts and Unloading Constraints
│   │   └── Plugin Architecture in Depth → Extensibility Group
│   │
│   ├── 13.09 REFERENCE ASSEMBLIES AND API CONTRACTS
│   │   ├── Compile-Time Reference Assemblies
│   │   ├── Runtime Implementation Assemblies
│   │   ├── Public API Surface and Implementation Details
│   │   ├── Targeting Packs and Framework References
│   │   ├── Facades and Compatibility Contracts
│   │   └── Why a Reference Assembly Is Not a Runtime Implementation
│   │
│   └── 13.10 INSPECTION AND COMPATIBILITY FAILURES
│       ├── Missing Assemblies and Missing Native Dependencies
│       ├── MissingMethodException and TypeLoadException
│       ├── BadImageFormatException and Architecture Mismatches
│       ├── ReflectionTypeLoadException and Loader Exceptions
│       ├── Inspecting Published Dependencies
│       ├── Comparing API Surfaces between Versions
│       └── Separating Build Success from Runtime Compatibility
│
└── 14. .NET HOSTING
    │
    ├── 14.01 HOSTING TERMINOLOGY
    │   ├── Operating-System Process
    │   ├── Native Runtime Host
    │   ├── dotnet Command-Line Host
    │   ├── Application-Specific Apphost
    │   ├── Runtime Hosting versus Generic Host
    │   └── Runtime Hosting versus ASP.NET Core Web Hosting
    │
    ├── 14.02 APPLICATION STARTUP
    │   ├── Starting an Apphost Executable
    │   ├── Starting an Application with dotnet Application.dll
    │   ├── Locating and Initializing the Runtime
    │   ├── hostfxr and hostpolicy Responsibilities
    │   ├── Resolving Frameworks and Application Dependencies
    │   ├── Loading the Entry Assembly
    │   └── Passing Arguments and Returning Exit Codes
    │
    ├── 14.03 HOST CONFIGURATION FILES
    │   ├── Application.runtimeconfig.json
    │   ├── Application.deps.json
    │   ├── Framework Requirements and Runtime Settings
    │   ├── Managed, Native, and Resource Dependencies
    │   ├── Environment-Based Host Configuration
    │   └── Build-Generated Configuration versus Manual Overrides
    │
    ├── 14.04 SDK AND RUNTIME SELECTION
    │   ├── Installed SDKs versus Installed Runtimes
    │   ├── global.json and SDK Selection
    │   ├── Requested Shared Framework Versions
    │   ├── Runtime Roll-Forward Policies
    │   ├── Side-by-Side Framework Resolution
    │   ├── Architecture and Installation Location
    │   └── Diagnosing Missing or Incompatible Runtime Errors
    │
    ├── 14.05 FRAMEWORK-DEPENDENT DEPLOYMENT
    │   ├── Application Files and Shared Runtime Requirements
    │   ├── Portable DLL-Based Launch
    │   ├── Platform-Specific Apphost Launch
    │   ├── Runtime Installation on the Target Machine
    │   ├── Shared Runtime Servicing
    │   ├── Deployment Size and Environment Dependencies
    │   └── Compatibility Verification on a Clean Machine
    │
    ├── 14.06 SELF-CONTAINED DEPLOYMENT
    │   ├── Bundling the Runtime with the Application
    │   ├── Selecting the Target OS and Architecture
    │   ├── RID-Specific Runtime and Native Assets
    │   ├── Deployment Size and Startup Considerations
    │   ├── Runtime Security Updates and Republishing
    │   ├── Remaining Operating-System Dependencies
    │   └── Why Self-Contained Does Not Mean Universally Portable
    │
    ├── 14.07 SINGLE-FILE DEPLOYMENT
    │   ├── Bundling Application Components
    │   ├── Framework-Dependent and Self-Contained Combinations
    │   ├── Native Libraries and Extraction Behavior
    │   ├── Content Files and External Configuration
    │   ├── File-Location Assumptions and Compatibility
    │   ├── Startup and Bundle-Size Tradeoffs
    │   └── Single-File Packaging versus Native Compilation
    │
    ├── 14.08 READYTORUN DEPLOYMENT
    │   ├── Precompiled Native Code within Managed Deployment
    │   ├── Startup Benefits and Increased Artifact Size
    │   ├── Runtime and Architecture Compatibility
    │   ├── Methods That Still Require JIT Compilation
    │   ├── Interaction with Tiered Compilation
    │   └── Measuring ReadyToRun against Ordinary Deployment
    │
    ├── 14.09 TRIMMING
    │   ├── Removing Unused Code during Publishing
    │   ├── Static Reachability Analysis
    │   ├── Reflection and Dynamically Accessed Members
    │   ├── Trimming Annotations and Analyzer Warnings
    │   ├── Serialization and Library Compatibility
    │   ├── Why Warning Suppression Does Not Prove Correctness
    │   └── Testing the Actual Trimmed Artifact
    │
    ├── 14.10 NATIVE AOT DEPLOYMENT
    │   ├── Ahead-of-Time Compilation into Native Code
    │   ├── Target Platform and Native Toolchain Requirements
    │   ├── Startup, Memory, Throughput, and Binary-Size Tradeoffs
    │   ├── Reflection Metadata and Trimming Requirements
    │   ├── Runtime Code Generation and Dynamic Loading Limitations
    │   ├── Generic Instantiation and Library Compatibility
    │   ├── Native Debugging and Symbol Files
    │   └── Detailed AOT Engineering → Native Interop Group
    │
    ├── 14.11 EMBEDDING .NET IN NATIVE APPLICATIONS
    │   ├── Native Hosts That Initialize .NET
    │   ├── Host Discovery through nethost
    │   ├── Runtime Initialization through hostfxr
    │   ├── Invoking Managed Entry Points from Native Code
    │   ├── Configuration and Dependency Resolution
    │   └── Lifetime, Compatibility, and Error Boundaries
    │
    └── 14.12 DEPLOYMENT COMPARISON AND VERIFICATION
        ├── Framework-Dependent versus Self-Contained
        ├── Multi-File versus Single-File
        ├── JIT versus ReadyToRun versus Native AOT
        ├── Trimming as a Separate Publishing Decision
        ├── Test OS, Architecture, Native Dependencies, and Permissions
        ├── Measure Cold Start, Warm Throughput, Memory, and Artifact Size
        ├── Diagnose Startup Failures with Host Diagnostics
        └── Verify Updates, Rollback, and Clean-Machine Execution