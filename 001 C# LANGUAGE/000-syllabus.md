🟦 GROUP 01 — C# LANGUAGE & PROGRAMMING
│
├── 01. C# LANGUAGE FUNDAMENTALS
│   │
│   ├── 01.01 INTRODUCTION TO C# AND .NET
│   │   ├── What Is Programming? What Is C#?
│   │   ├── C# Language versus .NET Platform
│   │   ├── SDK, Runtime, Compiler, Libraries, and IDE
│   │   ├── Source Code → CIL / IL → Native Machine Code
│   │   ├── Binary Digits, Bytes, and Machine Instructions
│   │   ├── Compilation, JIT, and AOT Overview
│   │   └── Cross-Platform Execution and Platform Limitations
│   │
│   ├── 01.02 DEVELOPMENT ENVIRONMENT AND FIRST PROGRAM
│   │   ├── Installing and Checking the .NET SDK
│   │   ├── Visual Studio, VS Code, and Rider
│   │   ├── dotnet new console, build, run, and publish
│   │   ├── Project Folder, Program.cs, and .csproj
│   │   ├── Target Framework and Language Version
│   │   ├── Hello World and Program Execution
│   │   └── Compile-Time Errors, Runtime Errors, and Logic Errors
│   │
│   ├── 01.03 PROGRAM STRUCTURE
│   │   ├── Source Files, Namespaces, Types, and Members
│   │   ├── using Directives, Aliases, and Global Usings
│   │   ├── Main Method and Command-Line Arguments
│   │   ├── Top-Level Statements
│   │   ├── File-Scoped and Block-Scoped Namespaces
│   │   └── Statements, Semicolons, Braces, and Formatting
│   │
│   ├── 01.04 TOKENS AND LEXICAL ELEMENTS
│   │   ├── Keywords and Contextual Keywords
│   │   ├── Identifiers and Naming Rules
│   │   ├── Literals, Operators, and Punctuation
│   │   ├── Whitespace and Case Sensitivity
│   │   ├── Escaped Identifiers Using @
│   │   ├── Single-Line, Block, and XML Documentation Comments
│   │   └── Preprocessor Directives: #if, #define, #region, #nullable
│   │
│   ├── 01.05 VARIABLES AND CONSTANTS
│   │   ├── Declaration, Initialization, and Assignment
│   │   ├── Local Variables, Fields, and Parameters
│   │   ├── Definite Assignment and Default Values
│   │   ├── const and Compile-Time Constants
│   │   ├── readonly Fields and Initialization Rules
│   │   ├── const versus readonly versus static readonly
│   │   └── Variable Scope, Lifetime, and Naming Conventions
│   │
│   ├── 01.06 BUILT-IN DATA TYPES
│   │   ├── Signed Integers: sbyte, short, int, long
│   │   ├── Unsigned Integers: byte, ushort, uint, ulong
│   │   ├── Native-Sized Integers: nint and nuint
│   │   ├── Floating-Point Types: float and double
│   │   ├── Decimal Arithmetic: decimal
│   │   ├── Boolean and Character Types: bool and char
│   │   ├── Reference Types: string and object
│   │   ├── Type Aliases: int versus System.Int32
│   │   └── Range, Precision, Overflow, Infinity, and NaN
│   │
│   ├── 01.07 VALUES, REFERENCES, AND COPYING
│   │   ├── Value Types versus Reference Types
│   │   ├── Copying a Value versus Copying a Reference
│   │   ├── Object Identity versus Value Equality
│   │   ├── Mutation and Shared References
│   │   ├── Boxing and Unboxing
│   │   └── Why Value Types Do Not Always Mean Stack Storage
│   │
│   ├── 01.08 LITERALS AND NUMBER REPRESENTATION
│   │   ├── Integer, Real, Boolean, Character, String, and Null Literals
│   │   ├── Decimal, Binary, and Hexadecimal Notation
│   │   ├── Numeric Suffixes: U, L, UL, F, D, M
│   │   ├── Digit Separators
│   │   └── Literal Type Selection and Constant Expressions
│   │
│   ├── 01.09 TYPE CONVERSION AND PARSING
│   │   ├── Implicit and Explicit Conversions
│   │   ├── Numeric Widening, Narrowing, and Truncation
│   │   ├── Cast Expressions and Convert APIs
│   │   ├── Parse and TryParse
│   │   ├── Culture-Aware and Invariant Parsing
│   │   ├── checked and unchecked
│   │   └── Conversion Failures and Safe Input Handling
│   │
│   ├── 01.10 OPERATORS AND EXPRESSIONS
│   │   ├── Arithmetic: +, -, *, /, %
│   │   ├── Assignment and Compound Assignment
│   │   ├── Prefix and Postfix Increment / Decrement
│   │   ├── Equality and Relational Operators
│   │   ├── Boolean Logic and Short-Circuit Evaluation
│   │   ├── Bitwise Operators and Bit Shifts
│   │   ├── Conditional Operator: ?:
│   │   ├── Type Operators: is, as, typeof, sizeof
│   │   ├── nameof and default Expressions
│   │   └── Precedence, Associativity, and Evaluation Order
│   │
│   ├── 01.11 STATEMENTS, BLOCKS, AND SCOPE
│   │   ├── Declaration and Expression Statements
│   │   ├── Empty Statements and Nested Blocks
│   │   ├── Local Scope and Enclosing Scope
│   │   ├── Name Conflicts and Member Qualification
│   │   ├── Scope versus Lifetime versus Accessibility
│   │   └── Reachable and Unreachable Code
│   │
│   ├── 01.12 CONDITIONS AND SELECTION
│   │   ├── if
│   │   ├── if–else
│   │   ├── else-if Chains
│   │   ├── Nested Conditions
│   │   ├── switch Statements, case, and default
│   │   ├── Guard Clauses and Early Return
│   │   └── Boundary Conditions and Boolean Reasoning
│   │
│   ├── 01.13 LOOPS AND ITERATION
│   │   ├── for Loops
│   │   ├── while Loops
│   │   ├── do–while Loops
│   │   ├── foreach Loops
│   │   ├── Nested Loops
│   │   ├── Infinite Loops and Termination Conditions
│   │   ├── Off-by-One Errors
│   │   └── Choosing the Appropriate Loop
│   │
│   ├── 01.14 CONTROL TRANSFER
│   │   ├── break
│   │   ├── continue
│   │   ├── return
│   │   ├── goto and Labels
│   │   ├── goto case and goto default
│   │   └── Control Flow in Nested Loops and switch Statements
│   │
│   ├── 01.15 NULL AND NULLABLE REFERENCE TYPES
│   │   ├── Meaning of null
│   │   ├── Nullable Contexts and Compiler Analysis
│   │   ├── string versus string?
│   │   ├── Null Checks and Flow Analysis
│   │   ├── Null-Conditional Access: ?. and ?[]
│   │   ├── Null-Coalescing Operators: ?? and ??=
│   │   ├── Null-Forgiving Operator: !
│   │   └── NullReferenceException and API Null Contracts
│   │
│   ├── 01.16 var, object, AND dynamic
│   │   ├── Explicit Typing versus Type Inference
│   │   ├── var Rules and Limitations
│   │   ├── Anonymous Types
│   │   ├── object and Runtime Type Checks
│   │   ├── dynamic and Runtime Member Binding
│   │   └── Compile-Time Safety and Appropriate Use Cases
│   │
│   ├── 01.17 STRINGS AND CONSOLE INPUT / OUTPUT
│   │   ├── String Immutability
│   │   ├── Concatenation, Interpolation, and Formatting
│   │   ├── Escape Sequences and Verbatim Strings
│   │   ├── Comparison, Searching, Splitting, and Joining
│   │   ├── Console.Write, WriteLine, and ReadLine
│   │   └── Reading and Validating User Input
│   │
│   └── 01.18 ARRAYS AND COLLECTION BASICS
│       ├── One-Dimensional Arrays
│       ├── Multidimensional and Jagged Arrays
│       ├── Indexing, Length, Bounds, and Iteration
│       ├── List<T>: Adding, Updating, Finding, and Removing
│       ├── Dictionary<TKey, TValue>: Keys and Values
│       ├── HashSet<T>: Unique Values
│       ├── Queue<T> and Stack<T>
│       └── Array versus List versus Dictionary versus Set
│
├── 02. OBJECT-ORIENTED PROGRAMMING
│   │
│   ├── 02.01 CLASSES AND OBJECTS
│   │   ├── Class Declarations and Object Creation
│   │   ├── State, Behavior, and Identity
│   │   ├── Instance Members and Static Members
│   │   └── Object References and Object Initializers
│   │
│   ├── 02.02 FIELDS AND PROPERTIES
│   │   ├── Instance Fields and Static Fields
│   │   ├── Backing Fields and Auto-Implemented Properties
│   │   ├── get and set Accessors
│   │   ├── Accessor Accessibility
│   │   ├── Read-Only and Computed Properties
│   │   └── Property Validation and Invariants
│   │
│   ├── 02.03 METHODS
│   │   ├── Declaration, Signature, Invocation, and Return Type
│   │   ├── Instance Methods and Static Methods
│   │   ├── Positional, Named, and Optional Arguments
│   │   ├── params Parameters
│   │   ├── Method Overloading and Overload Resolution
│   │   ├── Recursion and Base Cases
│   │   └── Extension Methods
│   │
│   ├── 02.04 CONSTRUCTORS AND INITIALIZATION
│   │   ├── Parameterless and Parameterized Constructors
│   │   ├── Constructor Overloading
│   │   ├── Constructor Chaining with this and base
│   │   ├── Static Constructors
│   │   ├── Field Initialization Order
│   │   └── Valid Object Construction
│   │
│   ├── 02.05 ACCESS MODIFIERS AND ENCAPSULATION
│   │   ├── public, private, protected, internal
│   │   ├── protected internal and private protected
│   │   ├── Type Accessibility versus Member Accessibility
│   │   ├── Hiding Internal State
│   │   └── Protecting Invariants through Methods and Properties
│   │
│   ├── 02.06 ABSTRACTION
│   │   ├── Exposing Capabilities and Hiding Implementation
│   │   ├── Contracts and Implementation Details
│   │   ├── Abstract Classes and Abstract Members
│   │   └── Choosing Appropriate Abstraction Boundaries
│   │
│   ├── 02.07 INHERITANCE
│   │   ├── Base Classes and Derived Classes
│   │   ├── Accessible Inherited Members
│   │   ├── this and base
│   │   ├── Constructor Execution across an Inheritance Hierarchy
│   │   ├── Upcasting and Downcasting
│   │   └── Inheritance versus Composition
│   │
│   ├── 02.08 POLYMORPHISM
│   │   ├── Compile-Time Overload Resolution
│   │   ├── Runtime Virtual Dispatch
│   │   ├── virtual and override
│   │   ├── Member Hiding with new
│   │   ├── sealed Classes and sealed Overrides
│   │   └── Declared Type versus Runtime Type
│   │
│   ├── 02.09 INTERFACES
│   │   ├── Interface Declarations and Implementation
│   │   ├── Multiple Interface Implementation
│   │   ├── Explicit Interface Implementation
│   │   ├── Interface Inheritance
│   │   ├── Default Interface Members
│   │   └── Interface versus Abstract Class
│   │
│   ├── 02.10 ADDITIONAL TYPE MEMBERS
│   │   ├── Indexers
│   │   ├── Nested Types
│   │   ├── Partial Classes and Partial Members
│   │   ├── Static Classes
│   │   └── Organizing Public and Internal APIs
│   │
│   ├── 02.11 OBJECT RELATIONSHIPS AND DESIGN
│   │   ├── Association, Aggregation, and Composition
│   │   ├── Dependency and Delegation
│   │   ├── Coupling and Cohesion
│   │   ├── Dependency Injection through Constructors
│   │   └── Modeling Responsibilities and Collaborations
│   │
│   └── 02.12 EQUALITY AND RESOURCE LIFETIME
│       ├── Equals, GetHashCode, and ToString
│       ├── Reference Equality versus Value Equality
│       ├── Equality Contracts and Collection Behavior
│       ├── Finalizer Syntax and Nondeterministic Finalization
│       ├── IDisposable, using, and Deterministic Cleanup
│       └── Resource Ownership versus Garbage Collection
│
├── 03. ADVANCED C# TYPES
│   │
│   ├── 03.01 STRUCTS
│   │   ├── Struct Declarations, Constructors, and Members
│   │   ├── Default Initialization
│   │   ├── Copying, Mutation, and Boxing
│   │   ├── readonly Structs and Readonly Members
│   │   └── Class versus Struct
│   │
│   ├── 03.02 RECORDS
│   │   ├── Record Classes and Record Structs
│   │   ├── Positional and Nonpositional Records
│   │   ├── Generated Members and Value Equality
│   │   ├── with Expressions and Shallow Copying
│   │   ├── Deconstruction
│   │   └── Record Inheritance and Immutability Limits
│   │
│   ├── 03.03 ENUMS
│   │   ├── Named Constants and Underlying Types
│   │   ├── Explicit Values and Default Values
│   │   ├── Parsing and Formatting
│   │   ├── FlagsAttribute and Bitwise Combinations
│   │   └── Undefined Values and Validation
│   │
│   ├── 03.04 TUPLES
│   │   ├── Tuple Syntax and Named Elements
│   │   ├── ValueTuple versus System.Tuple
│   │   ├── Returning Multiple Values
│   │   ├── Deconstruction and Discards
│   │   └── Tuple Equality and API Design Tradeoffs
│   │
│   ├── 03.05 DELEGATES
│   │   ├── Delegate Declarations and Signatures
│   │   ├── Method Groups and Delegate Conversion
│   │   ├── Single-Cast and Multicast Delegates
│   │   ├── Func, Action, and Predicate
│   │   ├── Anonymous Methods
│   │   └── Invocation Order, Return Values, and Exceptions
│   │
│   ├── 03.06 EVENTS
│   │   ├── Publisher and Subscriber Model
│   │   ├── event versus Delegate Fields
│   │   ├── EventHandler and EventHandler<TEventArgs>
│   │   ├── Subscribing, Unsubscribing, and Raising Events
│   │   ├── Custom Event Accessors
│   │   └── Subscriber Lifetime and Memory Retention
│   │
│   ├── 03.07 GENERICS
│   │   ├── Generic Classes, Structs, Interfaces, and Methods
│   │   ├── Type Parameters and Type Arguments
│   │   ├── Generic Type Inference
│   │   ├── Constraints: class, struct, notnull, unmanaged, new()
│   │   ├── Base-Class and Interface Constraints
│   │   ├── default(T) and Generic Nullability
│   │   └── Generic API Design and Avoiding Boxing
│   │
│   ├── 03.08 VARIANCE
│   │   ├── Invariance
│   │   ├── Covariance with out
│   │   ├── Contravariance with in
│   │   ├── Variance in Interfaces and Delegates
│   │   └── Reference-Type Restrictions and Array Covariance Risks
│   │
│   ├── 03.09 NULLABLE VALUE TYPES
│   │   ├── Nullable<T> and T?
│   │   ├── HasValue, Value, and GetValueOrDefault
│   │   ├── Lifted Operators and Nullable Comparisons
│   │   ├── Nullable Conversions and Boxing
│   │   └── Nullable Values versus Nullable Reference Annotations
│   │
│   ├── 03.10 PARAMETER PASSING AND REFERENCES
│   │   ├── Pass-by-Value for Values and Object References
│   │   ├── ref Parameters
│   │   ├── out Parameters
│   │   ├── in and ref readonly Parameters
│   │   ├── ref Locals and ref Returns
│   │   └── Aliasing, Copying Costs, and Lifetime Restrictions
│   │
│   └── 03.11 CUSTOM TYPE BEHAVIOR
│       ├── Operator Overloading
│       ├── User-Defined Conversion Operators
│       ├── IEquatable<T> and IComparable<T>
│       ├── Equality and Ordering Comparers
│       └── Consistent Semantics for Domain Types
│
├── 04. MODERN C# FEATURES
│   │
│   ├── 04.01 LAMBDA EXPRESSIONS
│   │   ├── Expression Lambdas and Statement Lambdas
│   │   ├── Parameter and Return-Type Inference
│   │   ├── Captured Variables and Closures
│   │   ├── Static Lambdas
│   │   └── Closure Lifetime, Mutation, and Allocation
│   │
│   ├── 04.02 PATTERN MATCHING
│   │   ├── Constant, Type, and Declaration Patterns
│   │   ├── Property and Extended Property Patterns
│   │   ├── Positional and Tuple Patterns
│   │   ├── Relational Patterns
│   │   ├── Logical Patterns: and, or, not
│   │   ├── List and Slice Patterns
│   │   └── var Patterns, Discards, and Pattern Variables
│   │
│   ├── 04.03 SWITCH EXPRESSIONS
│   │   ├── Expression Arms and Result Values
│   │   ├── when Guards
│   │   ├── Arm Ordering and Unreachable Patterns
│   │   ├── Exhaustiveness and Fallback Cases
│   │   └── switch Statement versus switch Expression
│   │
│   ├── 04.04 CONCISE MEMBERS AND LOCAL FUNCTIONS
│   │   ├── Expression-Bodied Methods and Properties
│   │   ├── Expression-Bodied Constructors and Accessors
│   │   ├── Local Functions and Static Local Functions
│   │   ├── Local Functions versus Lambdas
│   │   └── Readability and Debugging Tradeoffs
│   │
│   ├── 04.05 MODERN OBJECT INITIALIZATION
│   │   ├── init-Only Properties
│   │   ├── required Members
│   │   ├── SetsRequiredMembers and Its Contract
│   │   ├── Primary Constructors
│   │   ├── Target-Typed new Expressions
│   │   └── Initialization Requirements versus Runtime Validation
│   │
│   ├── 04.06 MODERN STRING SYNTAX
│   │   ├── Raw String Literals
│   │   ├── Multiline Indentation Rules
│   │   ├── Interpolated Raw Strings
│   │   ├── Quotes, Braces, and Delimiter Selection
│   │   └── Interpolated String Handler Concepts
│   │
│   ├── 04.07 COLLECTION EXPRESSIONS, INDICES, AND RANGES
│   │   ├── Collection Expressions: [...]
│   │   ├── Spread Elements: ..
│   │   ├── Target Typing and Supported Collection Shapes
│   │   ├── Indices from the End: ^
│   │   ├── Ranges and Slicing
│   │   └── Allocation, Copying, and View Semantics
│   │
│   └── 04.08 LANGUAGE EVOLUTION AND COMPATIBILITY
│       ├── Language Version versus SDK versus Target Framework
│       ├── Feature Availability and Compiler Diagnostics
│       ├── Extension Members and Extension Blocks
│       ├── Field-Backed Property Syntax
│       ├── Stable versus Preview Features
│       └── Adopting New Syntax without Breaking Compatibility
│
└── 05. C# ADVANCED PROGRAMMING
    │
    ├── 05.01 ITERATORS AND CUSTOM ENUMERATION
    │   ├── IEnumerable<T> and IEnumerator<T>
    │   ├── foreach Enumeration Pattern
    │   ├── yield return and yield break
    │   ├── Deferred Execution and Iterator State
    │   └── Iterator Cleanup and Repeated Enumeration
    │
    ├── 05.02 REFLECTION AND METADATA
    │   ├── Type, Assembly, and Member Information
    │   ├── Inspecting Constructors, Methods, Fields, and Properties
    │   ├── Creating Objects and Invoking Members
    │   ├── BindingFlags and Member Discovery
    │   └── Reflection Costs, Caching, and Trimming Compatibility
    │
    ├── 05.03 ATTRIBUTES
    │   ├── Built-In Attributes
    │   ├── Creating Custom Attributes
    │   ├── AttributeUsage, Targets, and Inheritance
    │   ├── Reading Attributes through Reflection
    │   └── Metadata Declarations versus Executable Behavior
    │
    ├── 05.04 EXPRESSION TREES
    │   ├── Delegates versus Expression<TDelegate>
    │   ├── Expression Nodes and Tree Structure
    │   ├── Creating, Inspecting, and Visiting Trees
    │   ├── Compiling Expression Trees
    │   └── Query Translation and Supported Expression Limitations
    │
    ├── 05.05 DYNAMIC OBJECT MODELS
    │   ├── Runtime Binding — Building on Chapter 01.16
    │   ├── ExpandoObject
    │   ├── DynamicObject
    │   ├── Dynamic Interoperability Scenarios
    │   └── Runtime Failures and Boundaries with Typed Code
    │
    ├── 05.06 MEMORY VIEWS AND BUFFER HANDLING
    │   ├── Span<T> and ReadOnlySpan<T>
    │   ├── Memory<T> and ReadOnlyMemory<T>
    │   ├── Slicing without Copying
    │   ├── Stack, Array, and Native-Backed Views
    │   ├── ArrayPool<T> and Memory Ownership
    │   └── Buffer Lifetime, Async Boundaries, and Readonly Limits
    │
    ├── 05.07 REF SAFETY AND ADVANCED GENERIC CONTRACTS
    │   ├── ref struct and readonly ref struct
    │   ├── scoped Parameters and Escape Analysis
    │   ├── Ref Fields and Lifetime Restrictions
    │   ├── Ref Struct Interfaces and allows ref struct
    │   ├── Static Abstract Interface Members
    │   └── Generic Math and Numeric Contracts
    │
    ├── 05.08 UNSAFE CODE
    │   ├── unsafe Contexts and Compiler Settings
    │   ├── Pointer Types, Address-of, and Dereferencing
    │   ├── Pointer Arithmetic and Bounds
    │   ├── fixed and Pinning
    │   ├── stackalloc
    │   ├── Managed and Unmanaged Function Pointers
    │   └── Alignment, Lifetime, and Memory-Corruption Risks
    │
    ├── 05.09 NATIVE INTEROPERABILITY FOUNDATIONS
    │   ├── Managed versus Native Boundaries
    │   ├── P/Invoke: LibraryImport and DllImport
    │   ├── ABI, Calling Conventions, and Structure Layout
    │   ├── String and Data Marshalling
    │   ├── Native Callbacks and Delegate Lifetime
    │   ├── SafeHandle and Resource Ownership
    │   └── OS, Architecture, and Native Dependency Compatibility
    │
    ├── 05.10 SOURCE GENERATION AND COMPILER EXTENSIBILITY
    │   ├── Runtime Reflection versus Compile-Time Generation
    │   ├── Roslyn Syntax Trees and Semantic Models
    │   ├── Incremental Source Generator Concepts
    │   ├── Generated Partial Types and Members
    │   ├── Compiler Diagnostics and Analyzer Concepts
    │   └── Detailed Generator Engineering → Dedicated Roslyn Group
    │
    └── 05.11 PRACTICAL C# DESIGN AND REVIEW
        ├── Choose Classes, Structs, Records, or Interfaces
        ├── Define Ownership, Nullability, and Mutation Contracts
        ├── Design Generic APIs and Consistent Equality
        ├── Avoid Unnecessary Reflection, dynamic, and Unsafe Code
        ├── Review Allocation, Copying, and Lifetime Behavior
        └── Build and Test a Reusable C# Library