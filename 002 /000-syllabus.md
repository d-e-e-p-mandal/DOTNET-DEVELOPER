```text
🟩 GROUP 02 — LINQ & FUNCTIONAL PROGRAMMING
│
├── 06. LINQ FUNDAMENTALS
│   │
│   ├── 06.01 INTRODUCTION TO LINQ
│   │   ├── LINQ Meaning
│   │   ├── Language Integrated Query
│   │   ├── Purpose of LINQ
│   │   ├── Why LINQ Was Introduced
│   │   ├── Declarative Querying
│   │   ├── Querying Objects
│   │   ├── Querying Collections
│   │   ├── Querying Arrays
│   │   ├── Querying Lists
│   │   ├── Querying Dictionaries
│   │   ├── Querying Sets
│   │   ├── Querying XML
│   │   ├── Querying Provider-Backed Sources
│   │   ├── Querying Databases through Providers
│   │   ├── Imperative Loops vs Declarative Queries
│   │   ├── LINQ to Objects
│   │   ├── Provider-Based LINQ
│   │   ├── Standard Query Operators
│   │   ├── LINQ Extension Methods
│   │   ├── Query Expressions
│   │   ├── Method Chains
│   │   ├── Query Composition
│   │   ├── System.Linq Namespace
│   │   ├── Enumerable Class
│   │   ├── Queryable Class
│   │   ├── Source → Query → Execution → Result
│   │   └── When to Use LINQ
│   │
│   ├── 06.02 LINQ ARCHITECTURE, SEQUENCES & TERMINOLOGY
│   │   ├── LINQ Architecture
│   │   │   ├── Data Source
│   │   │   ├── Source Sequence
│   │   │   ├── Query
│   │   │   ├── Query Operators
│   │   │   ├── Query Pipeline
│   │   │   ├── Intermediate Operations
│   │   │   ├── Terminal Operations
│   │   │   ├── Result Sequence
│   │   │   ├── Enumeration
│   │   │   └── Materialization
│   │   │
│   │   ├── LINQ Terminology
│   │   │   ├── Source
│   │   │   ├── Sequence
│   │   │   ├── Element
│   │   │   ├── Query
│   │   │   ├── Query Expression
│   │   │   ├── Query Operator
│   │   │   ├── Standard Query Operator
│   │   │   ├── Predicate
│   │   │   ├── Selector
│   │   │   ├── Key Selector
│   │   │   ├── Element Selector
│   │   │   ├── Collection Selector
│   │   │   ├── Result Selector
│   │   │   ├── Accumulator
│   │   │   ├── Comparer
│   │   │   ├── Equality Comparer
│   │   │   ├── Range Variable
│   │   │   ├── Query Provider
│   │   │   ├── Enumeration
│   │   │   ├── Materialization
│   │   │   ├── Deferred Execution
│   │   │   ├── Immediate Execution
│   │   │   ├── Streaming
│   │   │   ├── Buffering
│   │   │   ├── Filtering
│   │   │   ├── Projection
│   │   │   ├── Flattening
│   │   │   ├── Ordering
│   │   │   ├── Partitioning
│   │   │   ├── Grouping
│   │   │   ├── Joining
│   │   │   ├── Aggregation
│   │   │   └── Quantification
│   │   │
│   │   ├── IEnumerable
│   │   ├── IEnumerable<T>
│   │   ├── IEnumerator
│   │   ├── IEnumerator<T>
│   │   ├── GetEnumerator()
│   │   ├── MoveNext()
│   │   ├── Current
│   │   ├── IDisposable
│   │   ├── Enumeration through foreach
│   │   ├── Arrays as Enumerable Sources
│   │   ├── Collections as Enumerable Sources
│   │   ├── Custom Enumerable Sources
│   │   ├── yield return Sources
│   │   ├── Finite Sequences
│   │   ├── Empty Sequences
│   │   ├── Potentially Infinite Sequences
│   │   ├── Reusable Sources
│   │   ├── Single-Pass Sources
│   │   ├── Enumeration State
│   │   ├── Enumerator Lifetime
│   │   ├── Enumerator Disposal
│   │   ├── Re-enumeration
│   │   └── Source Mutation during Enumeration
│   │
│   ├── 06.03 QUERY SYNTAX, METHOD SYNTAX & KEYWORDS
│   │   ├── LINQ Syntax Forms
│   │   │   ├── Query Syntax
│   │   │   ├── Method Syntax
│   │   │   ├── Mixed Syntax
│   │   │   └── Fluent Method Chaining
│   │   │
│   │   ├── Query Contextual Keywords
│   │   │   ├── from
│   │   │   ├── where
│   │   │   ├── select
│   │   │   ├── orderby
│   │   │   ├── ascending
│   │   │   ├── descending
│   │   │   ├── group
│   │   │   ├── by
│   │   │   ├── join
│   │   │   ├── on
│   │   │   ├── equals
│   │   │   ├── into
│   │   │   └── let
│   │   │
│   │   ├── Supporting C# Keyword
│   │   │   └── in
│   │   │
│   │   ├── Query Expression Structure
│   │   │   ├── Initial from Clause
│   │   │   ├── Query Body
│   │   │   ├── Query Body Clauses
│   │   │   ├── Terminal select Clause
│   │   │   ├── Terminal group Clause
│   │   │   └── Query Continuation
│   │   │
│   │   ├── from Clause
│   │   │   ├── from x in source
│   │   │   ├── Source Expression
│   │   │   ├── Range Variable
│   │   │   ├── Implicitly Typed Range Variable
│   │   │   ├── Explicitly Typed Range Variable
│   │   │   ├── Multiple from Clauses
│   │   │   └── Nested Enumeration
│   │   │
│   │   ├── where Clause
│   │   │   ├── Boolean Predicate
│   │   │   ├── Comparison Expressions
│   │   │   ├── Logical Expressions
│   │   │   ├── Multiple Conditions
│   │   │   ├── Multiple where Clauses
│   │   │   └── Predicate Translation
│   │   │
│   │   ├── select Clause
│   │   │   ├── Selecting Whole Elements
│   │   │   ├── Selecting Properties
│   │   │   ├── Calculated Values
│   │   │   ├── Anonymous Types
│   │   │   ├── Tuples
│   │   │   ├── Records
│   │   │   ├── DTOs
│   │   │   └── Nested Projection
│   │   │
│   │   ├── orderby Clause
│   │   │   ├── Default Ascending Order
│   │   │   ├── ascending
│   │   │   ├── descending
│   │   │   ├── Multiple Keys
│   │   │   └── Stable Ordering
│   │   │
│   │   ├── group...by Clause
│   │   │   ├── Group Element
│   │   │   ├── Group Key
│   │   │   ├── Composite Key
│   │   │   ├── group x by key
│   │   │   └── group x by key into g
│   │   │
│   │   ├── join...on...equals Clause
│   │   │   ├── Outer Source
│   │   │   ├── Inner Source
│   │   │   ├── Outer Key
│   │   │   ├── Inner Key
│   │   │   ├── equals vs ==
│   │   │   ├── Inner Join
│   │   │   ├── Composite-Key Join
│   │   │   └── join...into
│   │   │
│   │   ├── let Clause
│   │   │   ├── Intermediate Values
│   │   │   ├── Calculated Values
│   │   │   ├── Reusing Expressions
│   │   │   └── let Variable Scope
│   │   │
│   │   ├── into Keyword
│   │   │   ├── Query Continuation
│   │   │   ├── Continuation after select
│   │   │   ├── Continuation after group
│   │   │   ├── Group Join Continuation
│   │   │   └── New Range Variable Scope
│   │   │
│   │   ├── Range Variables
│   │   │   ├── Declaration
│   │   │   ├── Type Inference
│   │   │   ├── Scope
│   │   │   ├── Multiple Range Variables
│   │   │   └── Transparent Identifiers
│   │   │
│   │   ├── Method Syntax
│   │   │   ├── Extension-Method Syntax
│   │   │   ├── Static-Method Syntax
│   │   │   ├── Lambda Arguments
│   │   │   ├── Method Chaining
│   │   │   ├── Predicate Arguments
│   │   │   ├── Selector Arguments
│   │   │   ├── Key Selector Arguments
│   │   │   ├── Collection Selector Arguments
│   │   │   ├── Result Selector Arguments
│   │   │   └── Comparer Arguments
│   │   │
│   │   ├── Query Translation
│   │   │   ├── where → Where
│   │   │   ├── select → Select
│   │   │   ├── Multiple from → SelectMany
│   │   │   ├── orderby → OrderBy
│   │   │   ├── Secondary orderby → ThenBy
│   │   │   ├── descending → OrderByDescending / ThenByDescending
│   │   │   ├── group...by → GroupBy
│   │   │   ├── join → Join
│   │   │   ├── join...into → GroupJoin
│   │   │   ├── Explicit Range Type → Cast<T>
│   │   │   ├── let → Intermediate Projection
│   │   │   └── into → Query Continuation
│   │   │
│   │   ├── Query Syntax vs Method Syntax
│   │   ├── Operators without Direct Query Syntax
│   │   ├── Combining Query and Method Syntax
│   │   ├── Nested Query Expressions
│   │   ├── Query Pattern
│   │   └── Compiler Query Translation
│   │
│   ├── 06.04 LAMBDA EXPRESSIONS & DELEGATES IN LINQ
│   │   ├── Lambda Role in LINQ
│   │   ├── Expression Lambda
│   │   │   └── x => expression
│   │   ├── Statement Lambda
│   │   │   └── x => { statements; }
│   │   ├── Multiple Parameters
│   │   │   └── (x, y) => expression
│   │   ├── Explicit Parameter Types
│   │   ├── Type Inference
│   │   ├── Func<T, TResult>
│   │   ├── Func<T, bool>
│   │   ├── Func<T, int, TResult>
│   │   ├── Predicate Functions
│   │   ├── Selectors
│   │   ├── Key Selectors
│   │   ├── Element Selectors
│   │   ├── Collection Selectors
│   │   ├── Result Selectors
│   │   ├── Accumulator Functions
│   │   ├── Named Methods as LINQ Arguments
│   │   ├── Lambdas as LINQ Arguments
│   │   ├── Captured Variables
│   │   ├── Closures
│   │   ├── Mutable Captures
│   │   ├── Static Lambdas
│   │   └── Delegate Allocation
│   │
│   ├── 06.05 FILTERING & TYPE SELECTION
│   │   ├── Where
│   │   │   ├── Predicate Filtering
│   │   │   ├── Where(Func<T,bool>)
│   │   │   ├── Indexed Where
│   │   │   ├── Multiple Conditions
│   │   │   ├── Multiple Where Calls
│   │   │   ├── Predicate Composition
│   │   │   ├── Conditional Filtering
│   │   │   ├── Null Filtering
│   │   │   └── Short-Circuit Expressions
│   │   ├── OfType<T>
│   │   │   ├── Runtime Type Filtering
│   │   │   ├── Mixed Collections
│   │   │   └── Inheritance Hierarchies
│   │   ├── Cast<T>
│   │   │   ├── Sequence Casting
│   │   │   ├── Runtime Cast
│   │   │   ├── InvalidCastException
│   │   │   └── Deferred Cast Failure
│   │   ├── Where vs OfType<T>
│   │   ├── Cast<T> vs OfType<T>
│   │   └── Predicate Ordering
│   │
│   ├── 06.06 PROJECTION & TRANSFORMATION
│   │   ├── Select
│   │   │   ├── Basic Projection
│   │   │   ├── Property Projection
│   │   │   ├── Computed Projection
│   │   │   ├── Indexed Select
│   │   │   ├── Anonymous-Type Projection
│   │   │   ├── Tuple Projection
│   │   │   ├── Record Projection
│   │   │   ├── DTO Projection
│   │   │   ├── Conditional Projection
│   │   │   ├── Null-Safe Projection
│   │   │   └── Nested Projection
│   │   ├── Projection vs Mutation
│   │   ├── Projection before Filtering
│   │   ├── Projection after Filtering
│   │   └── Narrow Projection
│   │
│   ├── 06.07 FLATTENING NESTED SEQUENCES
│   │   ├── SelectMany
│   │   ├── Select vs SelectMany
│   │   ├── Collection Selector
│   │   ├── Result Selector
│   │   ├── Indexed SelectMany
│   │   ├── Nested Collections
│   │   ├── Flattening
│   │   ├── Multiple from Clauses
│   │   ├── Parent–Child Projection
│   │   ├── Outer-Source Correlation
│   │   ├── Cartesian Products
│   │   ├── Nested SelectMany
│   │   ├── SelectMany-Based Joins
│   │   ├── Empty Inner Collections
│   │   └── Null Inner Collections
│   │
│   ├── 06.08 SORTING & ORDERING
│   │   ├── OrderBy
│   │   ├── OrderByDescending
│   │   ├── ThenBy
│   │   ├── ThenByDescending
│   │   ├── Reverse
│   │   ├── Primary Sort Key
│   │   ├── Secondary Sort Key
│   │   ├── Multiple Sort Keys
│   │   ├── IOrderedEnumerable<T>
│   │   ├── IComparer<T>
│   │   ├── Comparer<T>
│   │   ├── Custom Comparers
│   │   ├── StringComparer
│   │   ├── Case-Sensitive Ordering
│   │   ├── Case-Insensitive Ordering
│   │   ├── Culture-Aware Ordering
│   │   ├── Null Ordering
│   │   ├── Stable Ordering
│   │   ├── Replacing an Ordering
│   │   ├── Extending an Ordering
│   │   ├── OrderBy vs ThenBy
│   │   └── Reverse vs Descending Sort
│   │
│   ├── 06.09 PARTITIONING & PAGINATION
│   │   ├── Skip
│   │   ├── Take
│   │   ├── SkipWhile
│   │   ├── TakeWhile
│   │   ├── SkipLast
│   │   ├── TakeLast
│   │   ├── Chunk
│   │   ├── Range-Based Take
│   │   ├── Index-Aware Predicates
│   │   ├── Count-Based Partitioning
│   │   ├── Conditional Partitioning
│   │   ├── Early Termination
│   │   ├── Empty Results
│   │   ├── Pagination
│   │   ├── Offset Pagination
│   │   ├── Stable Ordering before Pagination
│   │   ├── Boundary Cases
│   │   └── Infinite-Sequence Partitioning
│   │
│   ├── 06.10 SEQUENCE CREATION & COMBINATION
│   │   ├── Enumerable.Empty<T>
│   │   ├── Enumerable.Range
│   │   ├── Enumerable.Repeat
│   │   ├── Append
│   │   ├── Prepend
│   │   ├── Concat
│   │   ├── Zip
│   │   ├── DefaultIfEmpty
│   │   ├── Generated Sequences
│   │   ├── Lazy Generation
│   │   ├── Infinite Sequence Concepts
│   │   ├── Repeated Object References
│   │   ├── Pairing by Position
│   │   ├── Unequal Sequence Lengths
│   │   ├── Concat vs Union
│   │   └── New Sequence vs Collection Mutation
│   │
│   ├── 06.11 QUERY EXECUTION
│   │   ├── Query Declaration
│   │   ├── Query Execution
│   │   ├── Deferred Execution
│   │   ├── Immediate Execution
│   │   ├── Lazy Evaluation
│   │   ├── Enumeration-Triggered Execution
│   │   ├── Materialization-Triggered Execution
│   │   ├── Scalar Terminal Operators
│   │   ├── Streaming Operators
│   │   ├── Buffering Operators
│   │   ├── Query Re-execution
│   │   ├── Repeated Enumeration
│   │   ├── Repeated Work
│   │   ├── Source Changes before Enumeration
│   │   ├── Captured Variables
│   │   ├── Side Effects
│   │   ├── Deferred Exceptions
│   │   ├── Early Termination
│   │   └── Infinite-Sequence Risks
│   │
│   ├── 06.12 MATERIALIZATION & CONVERSION
│   │   ├── ToArray
│   │   ├── ToList
│   │   ├── ToDictionary
│   │   ├── ToHashSet
│   │   ├── ToLookup
│   │   ├── AsEnumerable
│   │   ├── AsQueryable
│   │   ├── Cast
│   │   ├── OfType
│   │   ├── Immediate Materialization
│   │   ├── Snapshot Behavior
│   │   ├── Duplicate Dictionary Keys
│   │   ├── Dictionary Key Comparers
│   │   ├── Shallow Copies
│   │   ├── Shared Element References
│   │   ├── Deferred Sequence vs Materialized Result
│   │   └── Choosing the Correct Result Collection
│   │
│   ├── 06.13 IEnumerable<T>, IQueryable<T> & QUERY PROVIDERS
│   │   ├── IEnumerable<T>
│   │   │   ├── LINQ-to-Objects Foundation
│   │   │   ├── Delegate Execution
│   │   │   ├── CLR Execution
│   │   │   ├── In-Memory Evaluation
│   │   │   └── Enumerable Operators
│   │   ├── IQueryable<T>
│   │   │   ├── Queryable Sequences
│   │   │   ├── ElementType
│   │   │   ├── Expression
│   │   │   ├── Provider
│   │   │   ├── Expression Trees
│   │   │   ├── Provider Translation
│   │   │   └── Remote Execution
│   │   ├── IEnumerable<T> vs IQueryable<T>
│   │   │   ├── In-Memory vs Provider-Based
│   │   │   ├── Delegate vs Expression Tree
│   │   │   ├── Enumerable vs Queryable
│   │   │   ├── CLR vs Provider Execution
│   │   │   ├── Local vs Remote Evaluation
│   │   │   ├── Client-Side vs Server-Side Execution
│   │   │   ├── AsEnumerable Boundary
│   │   │   └── AsQueryable Boundary
│   │   ├── IQueryProvider
│   │   │   ├── CreateQuery
│   │   │   ├── CreateQuery<T>
│   │   │   ├── Execute
│   │   │   ├── Execute<TResult>
│   │   │   ├── Expression Interpretation
│   │   │   ├── Query Translation
│   │   │   └── Query Execution
│   │   ├── Provider Translation
│   │   ├── Provider Limitations
│   │   ├── Unsupported Expressions
│   │   ├── Translation Boundaries
│   │   ├── Provider-Specific Semantics
│   │   └── Custom Query Provider Concepts
│   │
│   ├── 06.14 EXPRESSION TREES IN LINQ
│   │   ├── Expression<TDelegate>
│   │   ├── Expression Trees vs Delegates
│   │   ├── LambdaExpression
│   │   ├── Expression Nodes
│   │   ├── ParameterExpression
│   │   ├── ConstantExpression
│   │   ├── MemberExpression
│   │   ├── MethodCallExpression
│   │   ├── BinaryExpression
│   │   ├── UnaryExpression
│   │   ├── ConditionalExpression
│   │   ├── Body
│   │   ├── Parameters
│   │   ├── Building Expression Trees
│   │   ├── Inspecting Expression Trees
│   │   ├── Combining Expressions
│   │   ├── Compiling Expressions
│   │   └── Query Provider Translation
│   │
│   └── 06.15 LINQ CORRECTNESS & PERFORMANCE
│       ├── Null Source vs Empty Sequence
│       ├── Null Elements
│       ├── Nullable Values
│       ├── Nullable Reference Types
│       ├── Default Values
│       ├── Multiple Enumeration
│       ├── Unnecessary Materialization
│       ├── Repeated Sorting
│       ├── Repeated Filtering
│       ├── Early Filtering
│       ├── Narrow Projection
│       ├── Any() vs Count() > 0
│       ├── First vs Single
│       ├── TryGetNonEnumeratedCount
│       ├── Iterator Overhead
│       ├── Delegate Overhead
│       ├── Closure Allocation
│       ├── Sorting Cost
│       ├── Buffering Cost
│       ├── Materialization Cost
│       ├── Memory Usage
│       ├── Large Sequences
│       ├── Side Effects in Queries
│       ├── Mutation during Enumeration
│       ├── Deferred-Execution Bugs
│       ├── IEnumerable/IQueryable Confusion
│       ├── Choosing LINQ vs Loop
│       └── Benchmarking Representative Queries
│
├── 07. LINQ AGGREGATION & GROUPING
│   │
│   ├── 07.01 COUNTING ELEMENTS
│   │   ├── Count
│   │   ├── LongCount
│   │   ├── Count()
│   │   ├── Count(predicate)
│   │   ├── LongCount()
│   │   ├── LongCount(predicate)
│   │   ├── Predicate-Based Counting
│   │   ├── Collection Count Property
│   │   ├── Array Length
│   │   ├── Query Counting
│   │   ├── Enumeration Costs
│   │   ├── Fast Count Paths
│   │   ├── TryGetNonEnumeratedCount
│   │   ├── Count vs LongCount
│   │   └── Count vs Any
│   │
│   ├── 07.02 NUMERIC AGGREGATION
│   │   ├── Sum
│   │   ├── Average
│   │   ├── Min
│   │   ├── Max
│   │   ├── Numeric Overloads
│   │   ├── Selector-Based Sum
│   │   ├── Selector-Based Average
│   │   ├── Selector-Based Min
│   │   ├── Selector-Based Max
│   │   ├── int
│   │   ├── long
│   │   ├── float
│   │   ├── double
│   │   ├── decimal
│   │   ├── Nullable Numeric Values
│   │   ├── Empty Sequence Behavior
│   │   ├── Overflow
│   │   ├── Precision
│   │   └── Rounding
│   │
│   ├── 07.03 SELECTING EXTREME ELEMENTS
│   │   ├── MinBy
│   │   ├── MaxBy
│   │   ├── Key Selector
│   │   ├── Selecting Element vs Key
│   │   ├── Custom Key Comparer
│   │   ├── Equal Keys
│   │   ├── Tie Behavior
│   │   ├── Null Keys
│   │   ├── Empty Sequence Behavior
│   │   └── Min/Max vs MinBy/MaxBy
│   │
│   ├── 07.04 CUSTOM AGGREGATION
│   │   ├── Aggregate
│   │   ├── Aggregate without Seed
│   │   ├── Aggregate with Seed
│   │   ├── Aggregate with Seed and Result Selector
│   │   ├── Seed
│   │   ├── Accumulator
│   │   ├── Accumulator Type
│   │   ├── Result Selector
│   │   ├── Running Totals
│   │   ├── String Construction
│   │   ├── Composite Summaries
│   │   ├── Mutable Accumulator
│   │   ├── Immutable Accumulator
│   │   ├── Associativity
│   │   ├── Order Dependence
│   │   └── Empty Sequence Behavior
│   │
│   ├── 07.05 QUANTIFIERS & MEMBERSHIP
│   │   ├── Any
│   │   │   ├── Any()
│   │   │   ├── Any(predicate)
│   │   │   └── Existence Checking
│   │   ├── All
│   │   │   ├── All(predicate)
│   │   │   └── Vacuous Truth on Empty Sequences
│   │   ├── Contains
│   │   │   ├── Default Equality
│   │   │   └── Custom Equality Comparer
│   │   ├── Short-Circuit Evaluation
│   │   ├── Membership Lookup Cost
│   │   ├── Any vs Count
│   │   └── Equality Semantics
│   │
│   ├── 07.06 ELEMENT RETRIEVAL
│   │   ├── First
│   │   ├── First(predicate)
│   │   ├── FirstOrDefault
│   │   ├── FirstOrDefault(predicate)
│   │   ├── FirstOrDefault with Explicit Default
│   │   ├── Last
│   │   ├── Last(predicate)
│   │   ├── LastOrDefault
│   │   ├── LastOrDefault(predicate)
│   │   ├── Single
│   │   ├── Single(predicate)
│   │   ├── SingleOrDefault
│   │   ├── SingleOrDefault(predicate)
│   │   ├── ElementAt
│   │   ├── ElementAtOrDefault
│   │   ├── Index-Based Element Access
│   │   ├── No-Match Behavior
│   │   ├── Multiple-Match Behavior
│   │   ├── Default Values as Valid Data
│   │   ├── Exceptions
│   │   ├── First vs Single
│   │   └── Expressing Expected Cardinality
│   │
│   ├── 07.07 GROUPING WITH GroupBy
│   │   ├── GroupBy
│   │   ├── IGrouping<TKey,TElement>
│   │   ├── Key Property
│   │   ├── Key Selector
│   │   ├── Element Selector
│   │   ├── Result Selector
│   │   ├── Equality Comparer
│   │   ├── Grouping by One Property
│   │   ├── Grouping by Multiple Properties
│   │   ├── Anonymous Composite Keys
│   │   ├── Tuple Keys
│   │   ├── Record Keys
│   │   ├── Custom Key Equality
│   │   ├── Nested Grouping
│   │   ├── Group Ordering
│   │   ├── Element Ordering within Groups
│   │   ├── Aggregation per Group
│   │   ├── Filtering before Grouping
│   │   ├── Filtering Groups after Aggregation
│   │   ├── group...by Query Syntax
│   │   ├── group...by...into Syntax
│   │   ├── Deferred Execution
│   │   └── Buffering Behavior
│   │
│   ├── 07.08 LOOKUPS WITH ToLookup
│   │   ├── ToLookup
│   │   ├── ILookup<TKey,TElement>
│   │   ├── Key Selector
│   │   ├── Element Selector
│   │   ├── Equality Comparer
│   │   ├── Immediate Lookup Construction
│   │   ├── One Key → Multiple Values
│   │   ├── Missing Keys
│   │   ├── Empty Results for Missing Keys
│   │   ├── Duplicate Keys
│   │   ├── ToLookup vs GroupBy
│   │   ├── ToLookup vs Dictionary
│   │   └── Repeated Lookup Performance
│   │
│   └── 07.09 GROUPED REPORTING & VALIDATION
│       ├── Count per Group
│       ├── Sum per Group
│       ├── Average per Group
│       ├── Minimum per Group
│       ├── Maximum per Group
│       ├── Multiple Aggregates per Group
│       ├── Filtering Groups
│       ├── Duplicate Detection
│       ├── Duplicate-Key Detection
│       ├── Top Element per Group
│       ├── Top N Elements per Group
│       ├── Nested Reports
│       ├── Date-Based Grouping
│       ├── Grouping by Day
│       ├── Grouping by Month
│       ├── Grouping by Year
│       ├── Missing Data
│       ├── Empty Inputs
│       ├── Boundary Values
│       └── Grouping Performance
│
├── 08. LINQ JOINS & SET OPERATIONS
│   │
│   ├── 08.01 JOIN FOUNDATIONS
│   │   ├── Join Concepts
│   │   ├── Outer Source
│   │   ├── Inner Source
│   │   ├── Join Key
│   │   ├── Outer Key Selector
│   │   ├── Inner Key Selector
│   │   ├── Result Selector
│   │   ├── Equality Comparer
│   │   ├── Matching Keys
│   │   ├── Missing Keys
│   │   ├── Duplicate Keys
│   │   ├── One-to-One Relationships
│   │   ├── One-to-Many Relationships
│   │   ├── Many-to-Many Relationships
│   │   ├── Join Cardinality
│   │   ├── Result Cardinality
│   │   ├── In-Memory Joins
│   │   └── Provider-Translated Joins
│   │
│   ├── 08.02 INNER JOINS
│   │   ├── Join
│   │   ├── Join Method Syntax
│   │   ├── join...on...equals Query Syntax
│   │   ├── Outer Key Selector
│   │   ├── Inner Key Selector
│   │   ├── Result Selector
│   │   ├── Anonymous Result Projection
│   │   ├── DTO Result Projection
│   │   ├── Composite-Key Join
│   │   ├── Anonymous-Type Composite Keys
│   │   ├── Custom Equality Comparer
│   │   ├── Duplicate-Key Multiplication
│   │   ├── Multiple Joins
│   │   ├── Nested Joins
│   │   └── Join Performance
│   │
│   ├── 08.03 GROUP JOINS
│   │   ├── GroupJoin
│   │   ├── join...into Query Syntax
│   │   ├── Outer Element
│   │   ├── Matching Inner Sequence
│   │   ├── Parent with Child Collection
│   │   ├── Empty Matching Groups
│   │   ├── GroupJoin Result Selector
│   │   ├── GroupJoin vs Join
│   │   ├── GroupJoin vs GroupBy
│   │   ├── Flattening GroupJoin
│   │   └── GroupJoin + SelectMany
│   │
│   ├── 08.04 OUTER JOINS & EXISTENCE QUERIES
│   │   ├── Left Outer Join
│   │   ├── GroupJoin + DefaultIfEmpty
│   │   ├── Query-Syntax Left Outer Join
│   │   ├── Method-Syntax Left Outer Join
│   │   ├── Missing Inner Elements
│   │   ├── Null Handling
│   │   ├── Right Outer Join by Reversing Sources
│   │   ├── Full Outer Join Construction
│   │   ├── Semi Join
│   │   ├── Records with a Match
│   │   ├── Anti Join
│   │   ├── Records without a Match
│   │   ├── Any-Based Existence Query
│   │   ├── Correlated Queries
│   │   ├── Preserving Duplicates
│   │   └── Preserving Ordering Semantics
│   │
│   ├── 08.05 EQUALITY & COMPARERS
│   │   ├── Equality Fundamentals
│   │   ├── EqualityComparer<T>.Default
│   │   ├── IEquatable<T>
│   │   ├── IEqualityComparer<T>
│   │   ├── Equals
│   │   ├── GetHashCode
│   │   ├── Equals/GetHashCode Contract
│   │   ├── Reference Identity
│   │   ├── Value Equality
│   │   ├── Records and Value Equality
│   │   ├── Anonymous-Type Equality
│   │   ├── Tuple Equality
│   │   ├── String Equality
│   │   ├── StringComparer.Ordinal
│   │   ├── StringComparer.OrdinalIgnoreCase
│   │   ├── Culture-Aware Comparisons
│   │   ├── Composite Keys
│   │   ├── Custom Comparers
│   │   ├── Hash-Based Operations
│   │   └── Mutable-Key Risks
│   │
│   ├── 08.06 DISTINCT OPERATIONS
│   │   ├── Distinct
│   │   ├── DistinctBy
│   │   ├── Default Equality
│   │   ├── Custom Equality
│   │   ├── Key-Based Distinctness
│   │   ├── Duplicate Elimination
│   │   ├── Distinct Objects
│   │   ├── Distinct by Property
│   │   └── Distinct vs GroupBy
│   │
│   ├── 08.07 SET OPERATIONS
│   │   ├── Union
│   │   ├── UnionBy
│   │   ├── Intersect
│   │   ├── IntersectBy
│   │   ├── Except
│   │   ├── ExceptBy
│   │   ├── Element-Based Operations
│   │   ├── Key-Based Operations
│   │   ├── Duplicate Elimination
│   │   ├── Equality Semantics
│   │   ├── Hashing
│   │   ├── Custom Comparers
│   │   ├── Deferred Execution
│   │   ├── Buffering
│   │   └── Ordering Considerations
│   │
│   ├── 08.08 SEQUENCE COMBINATION
│   │   ├── Concat
│   │   ├── Append
│   │   ├── Prepend
│   │   ├── Zip
│   │   ├── Zip with Tuples
│   │   ├── Pairing by Position
│   │   ├── Result Projection
│   │   ├── Unequal Sequence Lengths
│   │   ├── Combining Multiple Sequences
│   │   ├── Concat vs Union
│   │   └── Zip vs Join
│   │
│   ├── 08.09 SEQUENCE COMPARISON
│   │   ├── SequenceEqual
│   │   ├── Element Equality
│   │   ├── Sequence Length
│   │   ├── Element Order
│   │   ├── Duplicate Sensitivity
│   │   ├── Default Equality
│   │   ├── Custom Equality Comparer
│   │   ├── Sequence Equality vs Set Equality
│   │   ├── Ordered Comparison
│   │   ├── Unordered Comparison Strategies
│   │   ├── Short-Circuit Comparison
│   │   └── Enumeration Costs
│   │
│   └── 08.10 PRACTICAL DATA RECONCILIATION
│       ├── Compare Two Data Sources
│       ├── Find Added Records
│       ├── Find Removed Records
│       ├── Find Unchanged Records
│       ├── Find Modified Records
│       ├── Compare by Business Key
│       ├── Detect Duplicate Records
│       ├── Detect Missing Relationships
│       ├── Reconcile Imported Data
│       ├── Parent/Child Reconciliation
│       ├── Choose Join vs Lookup
│       ├── Choose Dictionary vs Lookup
│       ├── Choose HashSet vs Set Operators
│       ├── Avoid Cartesian Products
│       ├── Handle Duplicate Keys
│       ├── Handle Missing Keys
│       ├── Validate Result Cardinality
│       └── Test Boundary & Adversarial Data
│
└── 09. FUNCTIONAL C#
    │
    ├── 09.01 FUNCTIONAL PROGRAMMING FOUNDATIONS
    │   ├── Functional Programming
    │   ├── Functions as Values
    │   ├── First-Class Function Concepts
    │   ├── Declarative Programming
    │   ├── Declarative Data Transformation
    │   ├── Pure Functions
    │   ├── Impure Functions
    │   ├── Side Effects
    │   ├── Referential Transparency
    │   ├── Determinism
    │   ├── Explicit Inputs
    │   ├── Explicit Outputs
    │   ├── Immutability
    │   ├── Function Composition
    │   ├── Higher-Order Functions
    │   ├── Expression-Oriented Design
    │   ├── Data Transformation Pipelines
    │   ├── Functional Core
    │   ├── Imperative Shell
    │   └── Functional + Object-Oriented C#
    │
    ├── 09.02 DELEGATES AS FUNCTION CONTRACTS
    │   ├── Delegate Concept
    │   ├── Func<TResult>
    │   ├── Func<T,TResult>
    │   ├── Func<T1,T2,TResult>
    │   ├── Multi-Parameter Func
    │   ├── Action
    │   ├── Action<T>
    │   ├── Multi-Parameter Action
    │   ├── Predicate<T>
    │   ├── Named Methods
    │   ├── Anonymous Functions
    │   ├── Lambda Expressions
    │   ├── Passing Functions as Arguments
    │   ├── Returning Functions from Methods
    │   ├── Storing Functions in Variables
    │   ├── Storing Functions in Collections
    │   ├── Function Contracts
    │   ├── Transformation Functions
    │   ├── Predicate Functions
    │   └── Behavior Injection
    │
    ├── 09.03 HIGHER-ORDER FUNCTIONS
    │   ├── Definition of Higher-Order Function
    │   ├── Functions Accepting Functions
    │   ├── Functions Returning Functions
    │   ├── Configurable Filtering
    │   ├── Configurable Transformation
    │   ├── Configurable Sorting
    │   ├── Configurable Validation
    │   ├── Configurable Calculation
    │   ├── Strategy through Functions
    │   ├── Behavior Injection without Inheritance
    │   ├── Function Factories
    │   ├── Reusable Behavior
    │   ├── Generic Higher-Order Functions
    │   └── Generality vs Readability
    │
    ├── 09.04 CLOSURES
    │   ├── Closure Concept
    │   ├── Captured Variables
    │   ├── Captured State
    │   ├── Capturing Local Variables
    │   ├── Capturing Parameters
    │   ├── Capturing this
    │   ├── Capturing Variable vs Value
    │   ├── Closure Lifetime
    │   ├── Mutable Captures
    │   ├── Loop-Variable Capture
    │   ├── Deferred Execution + Closures
    │   ├── Closure Allocation
    │   ├── Retained Objects
    │   ├── Thread-Safety Problems
    │   ├── Static Lambdas
    │   └── Explicit State instead of Capture
    │
    ├── 09.05 IMMUTABILITY
    │   ├── Immutable Values
    │   ├── Mutable Values
    │   ├── readonly Fields
    │   ├── Readonly References
    │   ├── init-Only Properties
    │   ├── Records
    │   ├── Record Structs
    │   ├── with Expressions
    │   ├── Non-Destructive Mutation
    │   ├── Shallow Immutability
    │   ├── Deep Immutability
    │   ├── Immutable Collections
    │   ├── Read-Only Collection Interfaces
    │   ├── Immutable Storage
    │   ├── Structural Sharing
    │   ├── Copying Tradeoffs
    │   ├── Immutable State
    │   ├── Concurrent Operations
    │   └── Benefits of Immutability
    │
    ├── 09.06 FUNCTION COMPOSITION
    │   ├── Function Composition Concept
    │   ├── Output → Input Composition
    │   ├── Transformation Pipelines
    │   ├── Chaining Functions
    │   ├── Forward Composition
    │   ├── Reverse Composition
    │   ├── Predicate Composition
    │   │   ├── AND
    │   │   ├── OR
    │   │   └── NOT
    │   ├── Partial Application
    │   ├── Currying Concepts
    │   ├── C# Currying Patterns
    │   ├── Function Factories
    │   ├── Composition Order
    │   ├── Type Compatibility
    │   ├── Generic Composition
    │   └── Avoiding Excessive Indirection
    │
    ├── 09.07 MAP, FILTER, FLATTEN & FOLD
    │   ├── Map Concept
    │   │   └── Select
    │   ├── Filter Concept
    │   │   └── Where
    │   ├── FlatMap / Bind Concept
    │   │   └── SelectMany
    │   ├── Fold Concept
    │   │   └── Aggregate
    │   ├── Mapping Pipelines
    │   ├── Filtering Pipelines
    │   ├── Flattening Pipelines
    │   ├── Folding Pipelines
    │   ├── Choosing Seeds
    │   ├── Accumulator Types
    │   ├── Associative Operations
    │   ├── Order-Dependent Operations
    │   └── Building Functional LINQ Pipelines
    │
    ├── 09.08 MODELING ABSENCE & FAILURE
    │   ├── Absence as Data
    │   ├── Failure as Data
    │   ├── Nullable Value Types
    │   ├── Nullable Reference Types
    │   ├── Try-Pattern APIs
    │   ├── bool + out Patterns
    │   ├── Option / Maybe Concept
    │   ├── Some / None Concept
    │   ├── Result Concept
    │   ├── Either Concept
    │   ├── Success Case
    │   ├── Failure Case
    │   ├── Mapping Successful Values
    │   ├── Binding Successful Values
    │   ├── Chaining Results
    │   ├── Fail-Fast Validation
    │   ├── Error Accumulation
    │   ├── Exceptions vs Explicit Results
    │   └── Library Types vs Custom Types
    │
    ├── 09.09 CONTROLLING SIDE EFFECTS
    │   ├── Side-Effect Concepts
    │   ├── Pure Computation
    │   ├── I/O as a Side Effect
    │   ├── Database Access
    │   ├── Network Access
    │   ├── File-System Access
    │   ├── Console I/O
    │   ├── Logging
    │   ├── Time
    │   ├── Randomness
    │   ├── Environment State
    │   ├── Configuration
    │   ├── Global State
    │   ├── Mutable Shared State
    │   ├── Functional Core / Imperative Shell
    │   ├── Dependency Injection of Effects
    │   ├── Explicit Time Input
    │   ├── Explicit Randomness Input
    │   ├── Explicit Configuration Input
    │   ├── Logging at Boundaries
    │   ├── Avoiding Side Effects in LINQ Predicates
    │   ├── Avoiding Side Effects in LINQ Selectors
    │   └── Avoiding Side Effects in Deferred Queries
    │
    ├── 09.10 RECURSION & STATE TRANSFORMATION
    │   ├── Recursion
    │   ├── Recursive Decomposition
    │   ├── Base Case
    │   ├── Recursive Case
    │   ├── Recursive Traversal
    │   ├── Trees
    │   ├── Nested Structures
    │   ├── Accumulator Parameters
    │   ├── State Transformation
    │   ├── Immutable State Transitions
    │   ├── Stack Depth
    │   ├── Stack Overflow Risk
    │   ├── Tail Recursion Concepts
    │   ├── Tail-Call Assumptions
    │   ├── Iterative Alternatives
    │   ├── Memoization
    │   ├── Cache Keys
    │   ├── Cache Lifetime
    │   └── Bounded Memoization
    │
    ├── 09.11 FUNCTIONAL PIPELINE DESIGN
    │   ├── Pipeline Inputs
    │   ├── Pipeline Outputs
    │   ├── Transformation Stages
    │   ├── Filtering Stages
    │   ├── Validation Stages
    │   ├── Aggregation Stages
    │   ├── Composition
    │   ├── Small Functions
    │   ├── Pure Functions
    │   ├── Reusable Functions
    │   ├── Explicit Dependencies
    │   ├── Immutable Intermediate Results
    │   ├── Error Propagation
    │   ├── Short-Circuiting
    │   ├── Pipeline Readability
    │   ├── Pipeline Debugging
    │   ├── Pipeline Performance
    │   └── LINQ Pipeline Design
    │
    ├── 09.12 TESTING FUNCTIONAL CODE
    │   ├── Deterministic Tests
    │   ├── Pure Function Testing
    │   ├── Input/Output Tests
    │   ├── Table-Driven Tests
    │   ├── Boundary Cases
    │   ├── Null Cases
    │   ├── Empty Inputs
    │   ├── Invalid Inputs
    │   ├── Duplicate Inputs
    │   ├── Property-Based Testing
    │   ├── Invariants
    │   ├── Identity Laws
    │   ├── Associativity Laws
    │   ├── Composition Laws
    │   ├── Testing Pipelines
    │   ├── Testing without I/O
    │   ├── Testing Failure Cases
    │   └── Testing Side-Effect Boundaries
    │
    └── 09.13 PRACTICAL LINQ & FUNCTIONAL DESIGN
        ├── Build Collection Query Pipelines
        ├── Build Search and Filtering Pipelines
        ├── Build Sorting and Pagination Pipelines
        ├── Build Reporting Queries
        ├── Build Grouped Reports
        ├── Build Aggregation Reports
        ├── Build Inner Joins
        ├── Build Group Joins
        ├── Build Left Outer Joins
        ├── Build Data Reconciliation Queries
        ├── Build Duplicate Detection
        ├── Build Lookup Tables
        ├── Build Dynamic Filters
        ├── Build Reusable Predicates
        ├── Build Reusable Projections
        ├── Build Composable Validation Rules
        ├── Build Pure Pricing Calculations
        ├── Build Pure Scoring Calculations
        ├── Transform Nested Data
        ├── Reconcile Two Data Sources by Business Key
        ├── Handle Null and Empty Inputs
        ├── Handle Duplicate Data
        ├── Handle Missing Relationships
        ├── Test Query Correctness
        ├── Measure Enumeration Costs
        ├── Measure Allocation Costs
        ├── Measure Materialization Costs
        ├── Diagnose Multiple Enumeration
        ├── Diagnose Deferred-Execution Bugs
        ├── Diagnose Closure Bugs
        ├── Refactor Imperative Loops into LINQ
        ├── Refactor Overcomplicated LINQ into Loops
        ├── Choose IEnumerable<T> vs IQueryable<T>
        ├── Choose GroupBy vs ToLookup
        ├── Choose Dictionary vs Lookup
        ├── Choose HashSet vs Set Operators
        ├── Choose First vs Single
        ├── Choose Any vs Count
        ├── Choose Select vs SelectMany
        ├── Choose Join vs GroupJoin
        ├── Choose Deferred vs Materialized Results
        ├── Choose LINQ vs foreach
        └── Choose LINQ vs a Different Data Structure
```