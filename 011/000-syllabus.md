🟩 GROUP 11 — DATABASE & DATA ACCESS
│   │
│   ├── 44. ADO.NET
│   │   │
│   │   ├── 44.01 ADO.NET FOUNDATIONS
│   │   │   ├── Data Providers
│   │   │   ├── Connections
│   │   │   ├── Commands
│   │   │   ├── Readers
│   │   │   └── Transactions
│   │   │
│   │   ├── 44.02 ADO.NET ARCHITECTURE
│   │   │   ├── Connected Model
│   │   │   ├── Disconnected Model
│   │   │   ├── Provider Model
│   │   │   ├── Database Server
│   │   │   └── Application Boundary
│   │   │
│   │   ├── 44.03 DATABASE PROVIDERS
│   │   │   ├── DbProviderFactory
│   │   │   ├── SQL Server Provider
│   │   │   ├── PostgreSQL Provider
│   │   │   ├── MySQL Provider
│   │   │   └── SQLite Provider
│   │   │
│   │   ├── 44.04 DBCONNECTION
│   │   │   ├── ConnectionString
│   │   │   ├── Open
│   │   │   ├── Close
│   │   │   ├── State
│   │   │   └── Database
│   │   │
│   │   ├── 44.05 PROVIDER-SPECIFIC CONNECTIONS
│   │   │   ├── SqlConnection
│   │   │   ├── NpgsqlConnection
│   │   │   ├── MySqlConnection
│   │   │   ├── OracleConnection
│   │   │   └── SqliteConnection
│   │   │
│   │   ├── 44.06 CONNECTION STRINGS
│   │   │   ├── Server
│   │   │   ├── Database
│   │   │   ├── Authentication
│   │   │   ├── Connection Options
│   │   │   └── Connection String Builders
│   │   │
│   │   ├── 44.07 CONNECTION LIFETIME
│   │   │   ├── Open Late
│   │   │   ├── Close Early
│   │   │   ├── IDisposable
│   │   │   ├── IAsyncDisposable
│   │   │   └── Scoped Usage
│   │   │
│   │   ├── 44.08 CONNECTION POOLING
│   │   │   ├── Connection Pools
│   │   │   ├── Pool Keys
│   │   │   ├── Pool Size
│   │   │   ├── Connection Reuse
│   │   │   └── Pool Exhaustion
│   │   │
│   │   ├── 44.09 ASYNCHRONOUS CONNECTIONS
│   │   │   ├── OpenAsync
│   │   │   ├── CloseAsync
│   │   │   ├── Cancellation
│   │   │   ├── Async Disposal
│   │   │   └── I/O Scalability
│   │   │
│   │   ├── 44.10 DBCOMMAND
│   │   │   ├── CommandText
│   │   │   ├── CommandType
│   │   │   ├── Connection
│   │   │   ├── Parameters
│   │   │   └── CommandTimeout
│   │   │
│   │   ├── 44.11 COMMAND EXECUTION
│   │   │   ├── ExecuteNonQuery
│   │   │   ├── ExecuteScalar
│   │   │   ├── ExecuteReader
│   │   │   ├── Async Variants
│   │   │   └── Result Semantics
│   │   │
│   │   ├── 44.12 PARAMETERIZED COMMANDS
│   │   │   ├── DbParameter
│   │   │   ├── Parameter Names
│   │   │   ├── Parameter Values
│   │   │   ├── Database Types
│   │   │   └── SQL Injection Prevention
│   │   │
│   │   ├── 44.13 PARAMETER TYPE MAPPING
│   │   │   ├── DbType
│   │   │   ├── Provider Types
│   │   │   ├── Size
│   │   │   ├── Precision / Scale
│   │   │   └── Nullable Values
│   │   │
│   │   ├── 44.14 STORED PROCEDURES
│   │   │   ├── CommandType.StoredProcedure
│   │   │   ├── Input Parameters
│   │   │   ├── Output Parameters
│   │   │   ├── Return Values
│   │   │   └── Result Sets
│   │   │
│   │   ├── 44.15 DBDATAREADER
│   │   │   ├── Forward-Only Reading
│   │   │   ├── Read
│   │   │   ├── Field Access
│   │   │   ├── Schema
│   │   │   └── Reader Lifetime
│   │   │
│   │   ├── 44.16 DATA READER FIELD ACCESS
│   │   │   ├── Ordinals
│   │   │   ├── Column Names
│   │   │   ├── GetValue
│   │   │   ├── GetFieldValue<T>
│   │   │   └── Typed Getters
│   │   │
│   │   ├── 44.17 NULL DATABASE VALUES
│   │   │   ├── DBNull
│   │   │   ├── IsDBNull
│   │   │   ├── Nullable Types
│   │   │   ├── Null Mapping
│   │   │   └── Default Handling
│   │   │
│   │   ├── 44.18 MULTIPLE RESULT SETS
│   │   │   ├── NextResult
│   │   │   ├── Multiple Queries
│   │   │   ├── Result Boundaries
│   │   │   ├── Result Mapping
│   │   │   └── Async Iteration
│   │   │
│   │   ├── 44.19 ASYNC DATA READING
│   │   │   ├── ExecuteReaderAsync
│   │   │   ├── ReadAsync
│   │   │   ├── NextResultAsync
│   │   │   ├── GetFieldValueAsync
│   │   │   └── Cancellation
│   │   │
│   │   ├── 44.20 DATASET
│   │   │   ├── DataSet
│   │   │   ├── DataTables
│   │   │   ├── Relations
│   │   │   ├── Constraints
│   │   │   └── Disconnected Data
│   │   │
│   │   ├── 44.21 DATATABLE
│   │   │   ├── Columns
│   │   │   ├── Rows
│   │   │   ├── Primary Keys
│   │   │   ├── Constraints
│   │   │   └── Expressions
│   │   │
│   │   ├── 44.22 DATAROW
│   │   │   ├── Field Values
│   │   │   ├── RowState
│   │   │   ├── Original Values
│   │   │   ├── Current Values
│   │   │   └── Row Editing
│   │   │
│   │   ├── 44.23 DATARELATION
│   │   │   ├── Parent Table
│   │   │   ├── Child Table
│   │   │   ├── Parent Columns
│   │   │   ├── Child Columns
│   │   │   └── Relational Navigation
│   │   │
│   │   ├── 44.24 DATA ADAPTERS
│   │   │   ├── DbDataAdapter
│   │   │   ├── SelectCommand
│   │   │   ├── InsertCommand
│   │   │   ├── UpdateCommand
│   │   │   └── DeleteCommand
│   │   │
│   │   ├── 44.25 DATASET FILL AND UPDATE
│   │   │   ├── Fill
│   │   │   ├── Data Mapping
│   │   │   ├── Row Changes
│   │   │   ├── Update
│   │   │   └── AcceptChanges
│   │   │
│   │   ├── 44.26 DBTRANSACTION
│   │   │   ├── BeginTransaction
│   │   │   ├── Commit
│   │   │   ├── Rollback
│   │   │   ├── Command Association
│   │   │   └── Transaction Lifetime
│   │   │
│   │   ├── 44.27 TRANSACTION FUNDAMENTALS
│   │   │   ├── Atomicity
│   │   │   ├── Consistency
│   │   │   ├── Isolation
│   │   │   ├── Durability
│   │   │   └── Transaction Boundaries
│   │   │
│   │   ├── 44.28 ISOLATION LEVELS
│   │   │   ├── Read Uncommitted
│   │   │   ├── Read Committed
│   │   │   ├── Repeatable Read
│   │   │   ├── Serializable
│   │   │   └── Snapshot Concepts
│   │   │
│   │   ├── 44.29 TRANSACTION FAILURES
│   │   │   ├── Deadlocks
│   │   │   ├── Timeouts
│   │   │   ├── Connection Failure
│   │   │   ├── Rollback
│   │   │   └── Unknown Outcomes
│   │   │
│   │   ├── 44.30 SAVEPOINTS
│   │   │   ├── Save
│   │   │   ├── Rollback to Savepoint
│   │   │   ├── Partial Recovery
│   │   │   ├── Provider Support
│   │   │   └── Transaction State
│   │   │
│   │   ├── 44.31 SYSTEM.TRANSACTIONS
│   │   │   ├── TransactionScope
│   │   │   ├── Ambient Transactions
│   │   │   ├── Complete
│   │   │   ├── Enlistment
│   │   │   └── Distributed Transaction Concepts
│   │   │
│   │   ├── 44.32 COMMAND TIMEOUTS
│   │   │   ├── CommandTimeout
│   │   │   ├── Long Queries
│   │   │   ├── Cancellation
│   │   │   ├── Timeout Exceptions
│   │   │   └── Operational Limits
│   │   │
│   │   ├── 44.33 DATABASE CANCELLATION
│   │   │   ├── CancellationToken
│   │   │   ├── Command Cancellation
│   │   │   ├── Client Cancellation
│   │   │   ├── Server Processing
│   │   │   └── Cleanup
│   │   │
│   │   ├── 44.34 DATABASE EXCEPTIONS
│   │   │   ├── DbException
│   │   │   ├── Provider Exceptions
│   │   │   ├── Error Codes
│   │   │   ├── Constraint Violations
│   │   │   └── Transient Errors
│   │   │
│   │   ├── 44.35 ADO.NET RETRIES
│   │   │   ├── Transient Failures
│   │   │   ├── Retryable Operations
│   │   │   ├── Backoff
│   │   │   ├── Transaction Boundaries
│   │   │   └── Duplicate-Safety
│   │   │
│   │   ├── 44.36 BATCH DATABASE OPERATIONS
│   │   │   ├── DbBatch
│   │   │   ├── Batch Commands
│   │   │   ├── Round Trips
│   │   │   ├── Parameters
│   │   │   └── Provider Support
│   │   │
│   │   ├── 44.37 BULK DATA OPERATIONS
│   │   │   ├── Bulk Insert
│   │   │   ├── Bulk Copy
│   │   │   ├── Batching
│   │   │   ├── Transaction Boundaries
│   │   │   └── Provider Capabilities
│   │   │
│   │   ├── 44.38 DATABASE TYPE MAPPING
│   │   │   ├── SQL Types
│   │   │   ├── CLR Types
│   │   │   ├── Numeric Precision
│   │   │   ├── Date / Time Types
│   │   │   └── Binary Types
│   │   │
│   │   ├── 44.39 LARGE VALUE STREAMING
│   │   │   ├── BLOB Data
│   │   │   ├── CLOB / Text Data
│   │   │   ├── SequentialAccess
│   │   │   ├── Stream APIs
│   │   │   └── Memory Efficiency
│   │   │
│   │   ├── 44.40 ADO.NET SECURITY
│   │   │   ├── Parameterization
│   │   │   ├── Credential Protection
│   │   │   ├── Transport Encryption
│   │   │   ├── Least Privilege
│   │   │   └── Sensitive Data Handling
│   │   │
│   │   ├── 44.41 ADO.NET PERFORMANCE
│   │   │   ├── Connection Pooling
│   │   │   ├── Query Round Trips
│   │   │   ├── Reader Streaming
│   │   │   ├── Batching
│   │   │   └── Allocation Control
│   │   │
│   │   ├── 44.42 ADO.NET DIAGNOSTICS
│   │   │   ├── Connection Timing
│   │   │   ├── Command Timing
│   │   │   ├── Query Errors
│   │   │   ├── Pooling Issues
│   │   │   └── Database Correlation
│   │   │
│   │   ├── 44.43 ADO.NET TESTING
│   │   │   ├── Integration Tests
│   │   │   ├── Test Databases
│   │   │   ├── Transaction Tests
│   │   │   ├── Failure Tests
│   │   │   └── Provider Tests
│   │   │
│   │   └── 44.44 ADO.NET ENGINEERING PRACTICES
│   │       ├── Parameterize Every Dynamic Value
│   │       ├── Keep Connections Short-Lived
│   │       ├── Stream Large Results
│   │       ├── Make Transaction Boundaries Explicit
│   │       └── Understand Provider-Specific Behavior
│   │
│   ├── 45. SQL DATABASES
│   │   │
│   │   ├── 45.01 RELATIONAL DATABASE FOUNDATIONS
│   │   │   ├── Tables
│   │   │   ├── Rows
│   │   │   ├── Columns
│   │   │   ├── Keys
│   │   │   └── Relationships
│   │   │
│   │   ├── 45.02 RELATIONAL DATA MODELING
│   │   │   ├── Entities
│   │   │   ├── Attributes
│   │   │   ├── Relationships
│   │   │   ├── Constraints
│   │   │   └── Schema Design
│   │   │
│   │   ├── 45.03 PRIMARY AND FOREIGN KEYS
│   │   │   ├── Primary Keys
│   │   │   ├── Foreign Keys
│   │   │   ├── Composite Keys
│   │   │   ├── Referential Integrity
│   │   │   └── Cascading Actions
│   │   │
│   │   ├── 45.04 DATABASE CONSTRAINTS
│   │   │   ├── NOT NULL
│   │   │   ├── UNIQUE
│   │   │   ├── CHECK
│   │   │   ├── DEFAULT
│   │   │   └── FOREIGN KEY
│   │   │
│   │   ├── 45.05 NORMALIZATION
│   │   │   ├── First Normal Form
│   │   │   ├── Second Normal Form
│   │   │   ├── Third Normal Form
│   │   │   ├── Functional Dependencies
│   │   │   └── Denormalization Trade-Offs
│   │   │
│   │   ├── 45.06 SQL DATA TYPES
│   │   │   ├── Numeric Types
│   │   │   ├── Character Types
│   │   │   ├── Date / Time Types
│   │   │   ├── Binary Types
│   │   │   └── Provider-Specific Types
│   │   │
│   │   ├── 45.07 SQL QUERY FUNDAMENTALS
│   │   │   ├── SELECT
│   │   │   ├── FROM
│   │   │   ├── WHERE
│   │   │   ├── ORDER BY
│   │   │   └── DISTINCT
│   │   │
│   │   ├── 45.08 SQL FILTERING
│   │   │   ├── Comparison Operators
│   │   │   ├── Logical Operators
│   │   │   ├── LIKE
│   │   │   ├── IN
│   │   │   └── NULL Predicates
│   │   │
│   │   ├── 45.09 SQL JOINS
│   │   │   ├── INNER JOIN
│   │   │   ├── LEFT JOIN
│   │   │   ├── RIGHT JOIN
│   │   │   ├── FULL JOIN
│   │   │   └── CROSS JOIN
│   │   │
│   │   ├── 45.10 SQL AGGREGATION
│   │   │   ├── COUNT
│   │   │   ├── SUM
│   │   │   ├── AVG
│   │   │   ├── GROUP BY
│   │   │   └── HAVING
│   │   │
│   │   ├── 45.11 SUBQUERIES
│   │   │   ├── Scalar Subqueries
│   │   │   ├── Correlated Subqueries
│   │   │   ├── EXISTS
│   │   │   ├── IN
│   │   │   └── Derived Tables
│   │   │
│   │   ├── 45.12 COMMON TABLE EXPRESSIONS
│   │   │   ├── CTE Syntax
│   │   │   ├── Query Decomposition
│   │   │   ├── Recursive CTEs
│   │   │   ├── Hierarchical Data
│   │   │   └── CTE Scope
│   │   │
│   │   ├── 45.13 WINDOW FUNCTIONS
│   │   │   ├── OVER
│   │   │   ├── PARTITION BY
│   │   │   ├── ROW_NUMBER
│   │   │   ├── Ranking Functions
│   │   │   └── Window Aggregates
│   │   │
│   │   ├── 45.14 DATA MODIFICATION
│   │   │   ├── INSERT
│   │   │   ├── UPDATE
│   │   │   ├── DELETE
│   │   │   ├── Upsert Concepts
│   │   │   └── Returning Generated Values
│   │   │
│   │   ├── 45.15 DATABASE TRANSACTIONS
│   │   │   ├── BEGIN
│   │   │   ├── COMMIT
│   │   │   ├── ROLLBACK
│   │   │   ├── Savepoints
│   │   │   └── Transaction Scope
│   │   │
│   │   ├── 45.16 ACID PROPERTIES
│   │   │   ├── Atomicity
│   │   │   ├── Consistency
│   │   │   ├── Isolation
│   │   │   ├── Durability
│   │   │   └── Failure Recovery
│   │   │
│   │   ├── 45.17 TRANSACTION ISOLATION
│   │   │   ├── Dirty Reads
│   │   │   ├── Non-Repeatable Reads
│   │   │   ├── Phantom Reads
│   │   │   ├── Snapshot Isolation
│   │   │   └── Serializable Execution
│   │   │
│   │   ├── 45.18 DATABASE LOCKING
│   │   │   ├── Shared Locks
│   │   │   ├── Exclusive Locks
│   │   │   ├── Lock Granularity
│   │   │   ├── Blocking
│   │   │   └── Lock Escalation
│   │   │
│   │   ├── 45.19 DEADLOCKS
│   │   │   ├── Circular Wait
│   │   │   ├── Deadlock Detection
│   │   │   ├── Victim Selection
│   │   │   ├── Retry
│   │   │   └── Prevention
│   │   │
│   │   ├── 45.20 INDEXES
│   │   │   ├── B-Tree Concepts
│   │   │   ├── Clustered Indexes
│   │   │   ├── Nonclustered Indexes
│   │   │   ├── Composite Indexes
│   │   │   └── Unique Indexes
│   │   │
│   │   ├── 45.21 INDEX DESIGN
│   │   │   ├── Selectivity
│   │   │   ├── Key Order
│   │   │   ├── Covering Indexes
│   │   │   ├── Filtered / Partial Indexes
│   │   │   └── Write Cost
│   │   │
│   │   ├── 45.22 QUERY EXECUTION PLANS
│   │   │   ├── Table Scans
│   │   │   ├── Index Seeks
│   │   │   ├── Joins
│   │   │   ├── Sorts
│   │   │   └── Estimated Cost
│   │   │
│   │   ├── 45.23 QUERY OPTIMIZATION
│   │   │   ├── SARGability
│   │   │   ├── Index Usage
│   │   │   ├── Join Strategy
│   │   │   ├── Cardinality
│   │   │   └── Query Rewriting
│   │   │
│   │   ├── 45.24 DATABASE VIEWS
│   │   │   ├── View Definition
│   │   │   ├── Abstraction
│   │   │   ├── Security
│   │   │   ├── Query Composition
│   │   │   └── Materialized View Concepts
│   │   │
│   │   ├── 45.25 STORED PROCEDURES
│   │   │   ├── Parameters
│   │   │   ├── Result Sets
│   │   │   ├── Transactions
│   │   │   ├── Error Handling
│   │   │   └── Execution Plans
│   │   │
│   │   ├── 45.26 DATABASE FUNCTIONS
│   │   │   ├── Scalar Functions
│   │   │   ├── Table-Valued Functions
│   │   │   ├── Built-In Functions
│   │   │   ├── Determinism
│   │   │   └── Query Integration
│   │   │
│   │   ├── 45.27 DATABASE TRIGGERS
│   │   │   ├── INSERT Triggers
│   │   │   ├── UPDATE Triggers
│   │   │   ├── DELETE Triggers
│   │   │   ├── Side Effects
│   │   │   └── Operational Risks
│   │   │
│   │   ├── 45.28 SQL SERVER
│   │   │   ├── SQL Server Engine
│   │   │   ├── T-SQL
│   │   │   ├── Databases / Schemas
│   │   │   ├── SQL Server Security
│   │   │   └── Microsoft.Data.SqlClient
│   │   │
│   │   ├── 45.29 SQL SERVER DATA TYPES
│   │   │   ├── bigint / int
│   │   │   ├── decimal
│   │   │   ├── nvarchar
│   │   │   ├── datetime2
│   │   │   └── uniqueidentifier
│   │   │
│   │   ├── 45.30 SQL SERVER FEATURES
│   │   │   ├── Identity Columns
│   │   │   ├── Sequences
│   │   │   ├── Temporal Tables
│   │   │   ├── JSON Support
│   │   │   └── Table-Valued Parameters
│   │   │
│   │   ├── 45.31 POSTGRESQL
│   │   │   ├── PostgreSQL Server
│   │   │   ├── Schemas
│   │   │   ├── PostgreSQL SQL
│   │   │   ├── Extensions
│   │   │   └── Npgsql
│   │   │
│   │   ├── 45.32 POSTGRESQL DATA TYPES
│   │   │   ├── Arrays
│   │   │   ├── UUID
│   │   │   ├── JSON / JSONB
│   │   │   ├── Range Types
│   │   │   └── User-Defined Types
│   │   │
│   │   ├── 45.33 POSTGRESQL FEATURES
│   │   │   ├── RETURNING
│   │   │   ├── Sequences
│   │   │   ├── Generated Columns
│   │   │   ├── Full-Text Search
│   │   │   └── Extensions
│   │   │
│   │   ├── 45.34 MYSQL
│   │   │   ├── MySQL Server
│   │   │   ├── SQL Dialect
│   │   │   ├── Storage Engines
│   │   │   ├── InnoDB
│   │   │   └── .NET Providers
│   │   │
│   │   ├── 45.35 MARIADB
│   │   │   ├── MariaDB Server
│   │   │   ├── MySQL Compatibility
│   │   │   ├── SQL Differences
│   │   │   ├── Storage Engines
│   │   │   └── .NET Connectivity
│   │   │
│   │   ├── 45.36 MYSQL / MARIADB FEATURES
│   │   │   ├── AUTO_INCREMENT
│   │   │   ├── JSON
│   │   │   ├── Generated Columns
│   │   │   ├── Full-Text Indexes
│   │   │   └── Upsert Syntax
│   │   │
│   │   ├── 45.37 ORACLE DATABASE
│   │   │   ├── Oracle Database
│   │   │   ├── Schemas
│   │   │   ├── SQL
│   │   │   ├── PL/SQL
│   │   │   └── Oracle .NET Provider
│   │   │
│   │   ├── 45.38 ORACLE FEATURES
│   │   │   ├── Sequences
│   │   │   ├── Identity Columns
│   │   │   ├── Packages
│   │   │   ├── REF CURSOR
│   │   │   └── Oracle-Specific Types
│   │   │
│   │   ├── 45.39 SQLITE
│   │   │   ├── Embedded Database
│   │   │   ├── Database Files
│   │   │   ├── SQLite SQL
│   │   │   ├── Microsoft.Data.Sqlite
│   │   │   └── Embedded Application Use
│   │   │
│   │   ├── 45.40 SQLITE CHARACTERISTICS
│   │   │   ├── Dynamic Typing
│   │   │   ├── Type Affinity
│   │   │   ├── File Locking
│   │   │   ├── WAL Mode
│   │   │   └── Concurrency Constraints
│   │   │
│   │   ├── 45.41 CROSS-DATABASE PORTABILITY
│   │   │   ├── SQL Dialects
│   │   │   ├── Data Types
│   │   │   ├── Identifier Rules
│   │   │   ├── Generated Values
│   │   │   └── Provider Features
│   │   │
│   │   ├── 45.42 DATABASE SCHEMA DESIGN
│   │   │   ├── Tables
│   │   │   ├── Keys
│   │   │   ├── Constraints
│   │   │   ├── Indexes
│   │   │   └── Naming Conventions
│   │   │
│   │   ├── 45.43 DATABASE PAGINATION
│   │   │   ├── OFFSET / LIMIT
│   │   │   ├── OFFSET / FETCH
│   │   │   ├── Keyset Pagination
│   │   │   ├── Stable Ordering
│   │   │   └── Large-Offset Costs
│   │   │
│   │   ├── 45.44 DATABASE CONCURRENCY
│   │   │   ├── Pessimistic Concurrency
│   │   │   ├── Optimistic Concurrency
│   │   │   ├── Version Columns
│   │   │   ├── Isolation
│   │   │   └── Conflict Handling
│   │   │
│   │   ├── 45.45 DATABASE SECURITY
│   │   │   ├── Authentication
│   │   │   ├── Authorization
│   │   │   ├── Roles
│   │   │   ├── Encryption
│   │   │   └── Least Privilege
│   │   │
│   │   ├── 45.46 SQL INJECTION
│   │   │   ├── Injection Mechanics
│   │   │   ├── Parameterization
│   │   │   ├── Dynamic SQL
│   │   │   ├── Identifier Handling
│   │   │   └── Defense
│   │   │
│   │   ├── 45.47 DATABASE BACKUP AND RECOVERY CONCEPTS
│   │   │   ├── Full Backups
│   │   │   ├── Incremental / Differential Backups
│   │   │   ├── Transaction Logs
│   │   │   ├── Point-in-Time Recovery
│   │   │   └── Restore Verification
│   │   │
│   │   ├── 45.48 DATABASE PERFORMANCE
│   │   │   ├── Query Latency
│   │   │   ├── Index Efficiency
│   │   │   ├── I/O
│   │   │   ├── Lock Contention
│   │   │   └── Connection Load
│   │   │
│   │   ├── 45.49 DATABASE OBSERVABILITY
│   │   │   ├── Query Duration
│   │   │   ├── Active Connections
│   │   │   ├── Blocking
│   │   │   ├── Deadlocks
│   │   │   └── Resource Utilization
│   │   │
│   │   ├── 45.50 DATABASE TESTING
│   │   │   ├── Schema Tests
│   │   │   ├── Query Tests
│   │   │   ├── Constraint Tests
│   │   │   ├── Transaction Tests
│   │   │   └── Performance Tests
│   │   │
│   │   └── 45.51 SQL DATABASE ENGINEERING PRACTICES
│   │       ├── Model Constraints in the Database
│   │       ├── Index from Real Query Patterns
│   │       ├── Inspect Execution Plans
│   │       ├── Keep Transactions Appropriately Short
│   │       └── Treat SQL Dialects as Real Differences
│   │
│   ├── 46. ENTITY FRAMEWORK CORE
│   │   │
│   │   ├── 46.01 EF CORE FOUNDATIONS
│   │   │   ├── Object-Relational Mapping
│   │   │   ├── Entity Model
│   │   │   ├── DbContext
│   │   │   ├── LINQ
│   │   │   └── Database Provider
│   │   │
│   │   ├── 46.02 EF CORE ARCHITECTURE
│   │   │   ├── Application Model
│   │   │   ├── EF Model
│   │   │   ├── Query Pipeline
│   │   │   ├── Change Tracker
│   │   │   └── Provider
│   │   │
│   │   ├── 46.03 EF CORE PROVIDERS
│   │   │   ├── SQL Server
│   │   │   ├── PostgreSQL
│   │   │   ├── SQLite
│   │   │   ├── MySQL / MariaDB
│   │   │   └── Provider Capabilities
│   │   │
│   │   ├── 46.04 DBCONTEXT
│   │   │   ├── DbContext
│   │   │   ├── Configuration
│   │   │   ├── Model
│   │   │   ├── ChangeTracker
│   │   │   └── SaveChanges
│   │   │
│   │   ├── 46.05 DBCONTEXT CONFIGURATION
│   │   │   ├── DbContextOptions
│   │   │   ├── OnConfiguring
│   │   │   ├── Provider Configuration
│   │   │   ├── Connection String
│   │   │   └── Logging Options
│   │   │
│   │   ├── 46.06 DBCONTEXT LIFETIME
│   │   │   ├── Unit of Work
│   │   │   ├── Scoped Lifetime
│   │   │   ├── Thread Safety
│   │   │   ├── Disposal
│   │   │   └── Context Boundaries
│   │   │
│   │   ├── 46.07 DBCONTEXT DEPENDENCY INJECTION
│   │   │   ├── AddDbContext
│   │   │   ├── Scoped Context
│   │   │   ├── Options Configuration
│   │   │   ├── Service Resolution
│   │   │   └── Lifetime Rules
│   │   │
│   │   ├── 46.08 DBCONTEXT FACTORY
│   │   │   ├── IDbContextFactory
│   │   │   ├── AddDbContextFactory
│   │   │   ├── Context Creation
│   │   │   ├── Explicit Disposal
│   │   │   └── Non-Request Workflows
│   │   │
│   │   ├── 46.09 DBCONTEXT POOLING
│   │   │   ├── AddDbContextPool
│   │   │   ├── Context Reuse
│   │   │   ├── State Reset
│   │   │   ├── Performance
│   │   │   └── Stateful Configuration Risks
│   │   │
│   │   ├── 46.10 DBSET
│   │   │   ├── DbSet<TEntity>
│   │   │   ├── Querying
│   │   │   ├── Add
│   │   │   ├── Update
│   │   │   └── Remove
│   │   │
│   │   ├── 46.11 ENTITY TYPES
│   │   │   ├── Entity Classes
│   │   │   ├── Keys
│   │   │   ├── Scalar Properties
│   │   │   ├── Navigation Properties
│   │   │   └── Entity State
│   │   │
│   │   ├── 46.12 ENTITY KEYS
│   │   │   ├── Primary Keys
│   │   │   ├── Composite Keys
│   │   │   ├── Alternate Keys
│   │   │   ├── Generated Keys
│   │   │   └── Key Conventions
│   │   │
│   │   ├── 46.13 ENTITY PROPERTIES
│   │   │   ├── Property Mapping
│   │   │   ├── Required Properties
│   │   │   ├── Maximum Length
│   │   │   ├── Precision
│   │   │   └── Column Types
│   │   │
│   │   ├── 46.14 VALUE GENERATION
│   │   │   ├── Generated Keys
│   │   │   ├── Identity Columns
│   │   │   ├── Sequences
│   │   │   ├── Default Values
│   │   │   └── Computed Values
│   │   │
│   │   ├── 46.15 ENTITY RELATIONSHIPS
│   │   │   ├── Principal
│   │   │   ├── Dependent
│   │   │   ├── Foreign Keys
│   │   │   ├── Navigations
│   │   │   └── Referential Integrity
│   │   │
│   │   ├── 46.16 ONE-TO-ONE RELATIONSHIPS
│   │   │   ├── Reference Navigations
│   │   │   ├── Foreign Key
│   │   │   ├── Principal Entity
│   │   │   ├── Dependent Entity
│   │   │   └── Required / Optional
│   │   │
│   │   ├── 46.17 ONE-TO-MANY RELATIONSHIPS
│   │   │   ├── Collection Navigation
│   │   │   ├── Reference Navigation
│   │   │   ├── Foreign Key
│   │   │   ├── Required Relationship
│   │   │   └── Optional Relationship
│   │   │
│   │   ├── 46.18 MANY-TO-MANY RELATIONSHIPS
│   │   │   ├── Collection Navigations
│   │   │   ├── Join Tables
│   │   │   ├── Skip Navigations
│   │   │   ├── Join Entities
│   │   │   └── Payload Properties
│   │   │
│   │   ├── 46.19 CASCADE BEHAVIOR
│   │   │   ├── Cascade
│   │   │   ├── Restrict
│   │   │   ├── SetNull
│   │   │   ├── Client Behavior
│   │   │   └── DeleteBehavior
│   │   │
│   │   ├── 46.20 DATA ANNOTATIONS
│   │   │   ├── Key
│   │   │   ├── Required
│   │   │   ├── MaxLength
│   │   │   ├── Column
│   │   │   └── ForeignKey
│   │   │
│   │   ├── 46.21 FLUENT API
│   │   │   ├── ModelBuilder
│   │   │   ├── Entity
│   │   │   ├── Property
│   │   │   ├── HasKey
│   │   │   └── Relationship Configuration
│   │   │
│   │   ├── 46.22 ENTITYTYPECONFIGURATION
│   │   │   ├── IEntityTypeConfiguration<T>
│   │   │   ├── Configure
│   │   │   ├── ApplyConfiguration
│   │   │   ├── Assembly Scanning
│   │   │   └── Mapping Organization
│   │   │
│   │   ├── 46.23 TABLE AND COLUMN MAPPING
│   │   │   ├── ToTable
│   │   │   ├── HasColumnName
│   │   │   ├── HasColumnType
│   │   │   ├── Schema
│   │   │   └── Database Naming
│   │   │
│   │   ├── 46.24 VALUE CONVERSIONS
│   │   │   ├── HasConversion
│   │   │   ├── Enum Conversion
│   │   │   ├── Value Objects
│   │   │   ├── Provider Representation
│   │   │   └── ValueConverter
│   │   │
│   │   ├── 46.25 VALUE COMPARERS
│   │   │   ├── ValueComparer
│   │   │   ├── Equality
│   │   │   ├── Hashing
│   │   │   ├── Snapshotting
│   │   │   └── Mutable Values
│   │   │
│   │   ├── 46.26 OWNED ENTITY TYPES
│   │   │   ├── Ownership
│   │   │   ├── OwnsOne
│   │   │   ├── OwnsMany
│   │   │   ├── Table Mapping
│   │   │   └── Aggregate Modeling
│   │   │
│   │   ├── 46.27 COMPLEX TYPES
│   │   │   ├── Structured Values
│   │   │   ├── Property Grouping
│   │   │   ├── Value Semantics
│   │   │   ├── Column Mapping
│   │   │   └── Domain Modeling
│   │   │
│   │   ├── 46.28 INHERITANCE MAPPING
│   │   │   ├── TPH
│   │   │   ├── TPT
│   │   │   ├── TPC
│   │   │   ├── Discriminators
│   │   │   └── Performance Trade-Offs
│   │   │
│   │   ├── 46.29 LINQ TO ENTITIES
│   │   │   ├── IQueryable<T>
│   │   │   ├── Expression Trees
│   │   │   ├── Query Translation
│   │   │   ├── SQL Generation
│   │   │   └── Query Execution
│   │   │
│   │   ├── 46.30 EF CORE FILTERING
│   │   │   ├── Where
│   │   │   ├── Predicates
│   │   │   ├── Parameters
│   │   │   ├── Dynamic Composition
│   │   │   └── SQL Translation
│   │   │
│   │   ├── 46.31 EF CORE PROJECTION
│   │   │   ├── Select
│   │   │   ├── DTO Projection
│   │   │   ├── Anonymous Types
│   │   │   ├── Column Selection
│   │   │   └── Server Evaluation
│   │   │
│   │   ├── 46.32 EF CORE ORDERING AND PAGINATION
│   │   │   ├── OrderBy
│   │   │   ├── ThenBy
│   │   │   ├── Skip
│   │   │   ├── Take
│   │   │   └── Keyset Strategies
│   │   │
│   │   ├── 46.33 EF CORE JOINS
│   │   │   ├── Navigation Queries
│   │   │   ├── Join
│   │   │   ├── GroupJoin
│   │   │   ├── Correlated Queries
│   │   │   └── Generated SQL
│   │   │
│   │   ├── 46.34 EF CORE AGGREGATES
│   │   │   ├── Count
│   │   │   ├── Sum
│   │   │   ├── Average
│   │   │   ├── Min / Max
│   │   │   └── GroupBy
│   │   │
│   │   ├── 46.35 EAGER LOADING
│   │   │   ├── Include
│   │   │   ├── ThenInclude
│   │   │   ├── Filtered Include
│   │   │   ├── Navigation Graphs
│   │   │   └── Query Size
│   │   │
│   │   ├── 46.36 EXPLICIT LOADING
│   │   │   ├── Entry
│   │   │   ├── Reference
│   │   │   ├── Collection
│   │   │   ├── Load
│   │   │   └── Query
│   │   │
│   │   ├── 46.37 LAZY LOADING
│   │   │   ├── Lazy Loading Proxies
│   │   │   ├── Navigation Access
│   │   │   ├── Additional Queries
│   │   │   ├── N+1 Risk
│   │   │   └── Lifetime Requirements
│   │   │
│   │   ├── 46.38 SPLIT AND SINGLE QUERIES
│   │   │   ├── AsSingleQuery
│   │   │   ├── AsSplitQuery
│   │   │   ├── Cartesian Explosion
│   │   │   ├── Round Trips
│   │   │   └── Consistency Trade-Offs
│   │   │
│   │   ├── 46.39 CHANGE TRACKING
│   │   │   ├── ChangeTracker
│   │   │   ├── EntityEntry
│   │   │   ├── State
│   │   │   ├── Original Values
│   │   │   └── Current Values
│   │   │
│   │   ├── 46.40 ENTITY STATES
│   │   │   ├── Detached
│   │   │   ├── Unchanged
│   │   │   ├── Added
│   │   │   ├── Modified
│   │   │   └── Deleted
│   │   │
│   │   ├── 46.41 TRACKING QUERIES
│   │   │   ├── Tracking
│   │   │   ├── Identity Resolution
│   │   │   ├── State Manager
│   │   │   ├── Entity Reuse
│   │   │   └── Update Scenarios
│   │   │
│   │   ├── 46.42 NO-TRACKING QUERIES
│   │   │   ├── AsNoTracking
│   │   │   ├── Read-Only Queries
│   │   │   ├── Reduced Tracking Cost
│   │   │   ├── Identity Resolution Option
│   │   │   └── Query Performance
│   │   │
│   │   ├── 46.43 ADDING ENTITIES
│   │   │   ├── Add
│   │   │   ├── AddRange
│   │   │   ├── Graph Addition
│   │   │   ├── Generated Keys
│   │   │   └── SaveChanges
│   │   │
│   │   ├── 46.44 UPDATING ENTITIES
│   │   │   ├── Tracked Updates
│   │   │   ├── Property Changes
│   │   │   ├── Attach
│   │   │   ├── Update
│   │   │   └── Disconnected Entities
│   │   │
│   │   ├── 46.45 DELETING ENTITIES
│   │   │   ├── Remove
│   │   │   ├── RemoveRange
│   │   │   ├── Entity State
│   │   │   ├── Cascade Delete
│   │   │   └── SaveChanges
│   │   │
│   │   ├── 46.46 SAVECHANGES
│   │   │   ├── DetectChanges
│   │   │   ├── SQL Generation
│   │   │   ├── Transaction
│   │   │   ├── Database Execution
│   │   │   └── State Acceptance
│   │   │
│   │   ├── 46.47 ASYNC EF CORE
│   │   │   ├── ToListAsync
│   │   │   ├── SingleAsync
│   │   │   ├── FirstOrDefaultAsync
│   │   │   ├── SaveChangesAsync
│   │   │   └── Cancellation
│   │   │
│   │   ├── 46.48 RAW SQL QUERIES
│   │   │   ├── FromSql
│   │   │   ├── SQL Queries
│   │   │   ├── Parameterization
│   │   │   ├── Entity Mapping
│   │   │   └── Composability
│   │   │
│   │   ├── 46.49 RAW SQL COMMANDS
│   │   │   ├── ExecuteSql
│   │   │   ├── Parameterization
│   │   │   ├── Rows Affected
│   │   │   ├── Database Operations
│   │   │   └── Injection Safety
│   │   │
│   │   ├── 46.50 EF CORE LOGGING
│   │   │   ├── Generated SQL
│   │   │   ├── Command Events
│   │   │   ├── Sensitive Data Logging
│   │   │   ├── Detailed Errors
│   │   │   └── Diagnostic Categories
│   │   │
│   │   └── 46.51 EF CORE ENGINEERING PRACTICES
│   │       ├── Keep DbContext Units of Work Short
│   │       ├── Project Only Required Data
│   │       ├── Understand Generated SQL
│   │       ├── Choose Tracking Deliberately
│   │       └── Model Database Constraints Explicitly
│   │
│   ├── 47. EF CORE ADVANCED
│   │   │
│   │   ├── 47.01 ADVANCED EF CORE MODELING
│   │   │   ├── Complex Models
│   │   │   ├── Database-Specific Mapping
│   │   │   ├── Advanced Relationships
│   │   │   ├── Domain Constraints
│   │   │   └── Model Trade-Offs
│   │   │
│   │   ├── 47.02 MIGRATIONS FOUNDATIONS
│   │   │   ├── Model Changes
│   │   │   ├── Migration Classes
│   │   │   ├── Up
│   │   │   ├── Down
│   │   │   └── Migration History
│   │   │
│   │   ├── 47.03 MIGRATION CREATION
│   │   │   ├── Add Migration
│   │   │   ├── Model Snapshot
│   │   │   ├── Generated Operations
│   │   │   ├── Migration Naming
│   │   │   └── Migration Review
│   │   │
│   │   ├── 47.04 MIGRATION APPLICATION
│   │   │   ├── Database Update
│   │   │   ├── Pending Migrations
│   │   │   ├── Migration Ordering
│   │   │   ├── Migration History Table
│   │   │   └── Target Migration
│   │   │
│   │   ├── 47.05 MIGRATION SCRIPTS
│   │   │   ├── SQL Script Generation
│   │   │   ├── Idempotent Scripts
│   │   │   ├── Script Review
│   │   │   ├── Deployment
│   │   │   └── Auditability
│   │   │
│   │   ├── 47.06 MIGRATION BUNDLES
│   │   │   ├── Migration Bundle
│   │   │   ├── Executable Migration
│   │   │   ├── Deployment Artifact
│   │   │   ├── Configuration
│   │   │   └── Controlled Execution
│   │   │
│   │   ├── 47.07 CUSTOM MIGRATIONS
│   │   │   ├── Custom SQL
│   │   │   ├── Data Transformation
│   │   │   ├── Rename Operations
│   │   │   ├── Provider-Specific SQL
│   │   │   └── Reversible Changes
│   │   │
│   │   ├── 47.08 DATA MIGRATIONS
│   │   │   ├── Backfills
│   │   │   ├── Data Transformation
│   │   │   ├── Default Population
│   │   │   ├── Batched Migration
│   │   │   └── Verification
│   │   │
│   │   ├── 47.09 ZERO-DOWNTIME SCHEMA EVOLUTION
│   │   │   ├── Expand
│   │   │   ├── Migrate
│   │   │   ├── Contract
│   │   │   ├── Backward Compatibility
│   │   │   └── Multi-Version Deployment
│   │   │
│   │   ├── 47.10 MIGRATION ROLLBACK STRATEGY
│   │   │   ├── Down Migrations
│   │   │   ├── Forward Fixes
│   │   │   ├── Data Loss Risk
│   │   │   ├── Backup Recovery
│   │   │   └── Rollback Planning
│   │   │
│   │   ├── 47.11 EF CORE TRANSACTIONS
│   │   │   ├── SaveChanges Transaction
│   │   │   ├── BeginTransaction
│   │   │   ├── Commit
│   │   │   ├── Rollback
│   │   │   └── Transaction Lifetime
│   │   │
│   │   ├── 47.12 EXPLICIT TRANSACTIONS
│   │   │   ├── Database.BeginTransaction
│   │   │   ├── Multiple SaveChanges
│   │   │   ├── CommitAsync
│   │   │   ├── RollbackAsync
│   │   │   └── Disposal
│   │   │
│   │   ├── 47.13 SAVEPOINTS
│   │   │   ├── CreateSavepoint
│   │   │   ├── RollbackToSavepoint
│   │   │   ├── ReleaseSavepoint
│   │   │   ├── Partial Recovery
│   │   │   └── Provider Support
│   │   │
│   │   ├── 47.14 SHARED TRANSACTIONS
│   │   │   ├── DbConnection
│   │   │   ├── DbTransaction
│   │   │   ├── UseTransaction
│   │   │   ├── Multiple Contexts
│   │   │   └── Connection Ownership
│   │   │
│   │   ├── 47.15 TRANSACTIONSCOPE WITH EF CORE
│   │   │   ├── Ambient Transactions
│   │   │   ├── TransactionScope
│   │   │   ├── Async Flow
│   │   │   ├── Enlistment
│   │   │   └── Provider Limitations
│   │   │
│   │   ├── 47.16 EXECUTION STRATEGIES
│   │   │   ├── Transient Failures
│   │   │   ├── Retry Strategy
│   │   │   ├── Provider Strategy
│   │   │   ├── Retry Boundaries
│   │   │   └── Idempotency
│   │   │
│   │   ├── 47.17 RETRIES AND TRANSACTIONS
│   │   │   ├── Execution Strategy
│   │   │   ├── Transaction Replay
│   │   │   ├── Commit Failure
│   │   │   ├── Unknown Outcome
│   │   │   └── Duplicate Safety
│   │   │
│   │   ├── 47.18 OPTIMISTIC CONCURRENCY
│   │   │   ├── Concurrency Tokens
│   │   │   ├── Original Values
│   │   │   ├── Conditional Updates
│   │   │   ├── Conflict Detection
│   │   │   └── DbUpdateConcurrencyException
│   │   │
│   │   ├── 47.19 ROWVERSION CONCURRENCY
│   │   │   ├── rowversion
│   │   │   ├── Timestamp Mapping
│   │   │   ├── IsRowVersion
│   │   │   ├── Generated Tokens
│   │   │   └── SQL Server Semantics
│   │   │
│   │   ├── 47.20 APPLICATION-MANAGED CONCURRENCY
│   │   │   ├── Version Properties
│   │   │   ├── GUID Tokens
│   │   │   ├── Token Regeneration
│   │   │   ├── Selective Concurrency
│   │   │   └── Provider Portability
│   │   │
│   │   ├── 47.21 CONCURRENCY CONFLICT RESOLUTION
│   │   │   ├── Client Wins
│   │   │   ├── Database Wins
│   │   │   ├── Merge
│   │   │   ├── Reload
│   │   │   └── Retry
│   │   │
│   │   ├── 47.22 GLOBAL QUERY FILTERS
│   │   │   ├── HasQueryFilter
│   │   │   ├── Automatic Predicates
│   │   │   ├── Context Data
│   │   │   ├── IgnoreQueryFilters
│   │   │   └── Filter Composition
│   │   │
│   │   ├── 47.23 SOFT DELETE
│   │   │   ├── IsDeleted
│   │   │   ├── Query Filters
│   │   │   ├── Delete Interception
│   │   │   ├── Restoration
│   │   │   └── Unique Constraint Issues
│   │   │
│   │   ├── 47.24 MULTI-TENANCY FILTERING
│   │   │   ├── Tenant Identifier
│   │   │   ├── Query Filters
│   │   │   ├── Context Tenant
│   │   │   ├── Data Isolation
│   │   │   └── Filter Bypass Risks
│   │   │
│   │   ├── 47.25 INTERCEPTORS
│   │   │   ├── EF Interception
│   │   │   ├── Interceptor Registration
│   │   │   ├── Before / After Hooks
│   │   │   ├── Suppression
│   │   │   └── Cross-Cutting Behavior
│   │   │
│   │   ├── 47.26 COMMAND INTERCEPTORS
│   │   │   ├── DbCommandInterceptor
│   │   │   ├── Command Execution
│   │   │   ├── SQL Inspection
│   │   │   ├── Timing
│   │   │   └── Command Modification
│   │   │
│   │   ├── 47.27 CONNECTION INTERCEPTORS
│   │   │   ├── DbConnectionInterceptor
│   │   │   ├── Opening
│   │   │   ├── Closing
│   │   │   ├── Connection Failures
│   │   │   └── Connection Instrumentation
│   │   │
│   │   ├── 47.28 SAVECHANGES INTERCEPTORS
│   │   │   ├── SaveChangesInterceptor
│   │   │   ├── Saving Changes
│   │   │   ├── Saved Changes
│   │   │   ├── Save Failures
│   │   │   └── Auditing
│   │   │
│   │   ├── 47.29 MATERIALIZATION INTERCEPTORS
│   │   │   ├── Entity Materialization
│   │   │   ├── Instance Creation
│   │   │   ├── Initialization
│   │   │   ├── Materialized Entities
│   │   │   └── Cross-Cutting Initialization
│   │   │
│   │   ├── 47.30 COMPILED QUERIES
│   │   │   ├── EF.CompileQuery
│   │   │   ├── EF.CompileAsyncQuery
│   │   │   ├── Query Compilation Cost
│   │   │   ├── Query Parameters
│   │   │   └── Reuse
│   │   │
│   │   ├── 47.31 QUERY COMPILATION
│   │   │   ├── Expression Trees
│   │   │   ├── Query Shape
│   │   │   ├── Translation
│   │   │   ├── Query Cache
│   │   │   └── Parameterization
│   │   │
│   │   ├── 47.32 QUERY TAGGING
│   │   │   ├── TagWith
│   │   │   ├── SQL Comments
│   │   │   ├── Query Identification
│   │   │   ├── Diagnostics
│   │   │   └── Production Correlation
│   │   │
│   │   ├── 47.33 BULK UPDATE AND DELETE
│   │   │   ├── ExecuteUpdate
│   │   │   ├── ExecuteDelete
│   │   │   ├── Set-Based Operations
│   │   │   ├── Change Tracker Bypass
│   │   │   └── Transaction Semantics
│   │   │
│   │   ├── 47.34 RAW SQL ADVANCED USAGE
│   │   │   ├── Complex SQL
│   │   │   ├── Stored Procedures
│   │   │   ├── Unmapped Results
│   │   │   ├── Parameterization
│   │   │   └── Provider-Specific Features
│   │   │
│   │   ├── 47.35 KEYLESS ENTITY TYPES
│   │   │   ├── HasNoKey
│   │   │   ├── Read-Only Models
│   │   │   ├── Database Views
│   │   │   ├── Query Results
│   │   │   └── Tracking Limitations
│   │   │
│   │   ├── 47.36 TABLE SPLITTING
│   │   │   ├── Shared Table
│   │   │   ├── Multiple Entities
│   │   │   ├── Shared Primary Key
│   │   │   ├── Column Mapping
│   │   │   └── Modeling Trade-Offs
│   │   │
│   │   ├── 47.37 ENTITY SPLITTING
│   │   │   ├── Single Entity
│   │   │   ├── Multiple Tables
│   │   │   ├── Property Mapping
│   │   │   ├── Table Fragments
│   │   │   └── Schema Constraints
│   │   │
│   │   ├── 47.38 JSON COLUMN MAPPING
│   │   │   ├── Structured Data
│   │   │   ├── JSON Columns
│   │   │   ├── Owned / Complex Structures
│   │   │   ├── Provider Translation
│   │   │   └── Querying JSON Data
│   │   │
│   │   ├── 47.39 TEMPORAL TABLES
│   │   │   ├── System-Versioned Tables
│   │   │   ├── Temporal Queries
│   │   │   ├── Historical Rows
│   │   │   ├── Period Columns
│   │   │   └── SQL Server Support
│   │   │
│   │   ├── 47.40 DATABASE FUNCTIONS
│   │   │   ├── DbFunction
│   │   │   ├── Function Mapping
│   │   │   ├── Built-In Functions
│   │   │   ├── User-Defined Functions
│   │   │   └── Query Translation
│   │   │
│   │   ├── 47.41 STORED PROCEDURE MAPPING
│   │   │   ├── Stored Procedures
│   │   │   ├── Insert Operations
│   │   │   ├── Update Operations
│   │   │   ├── Delete Operations
│   │   │   └── Provider Behavior
│   │   │
│   │   ├── 47.42 EF CORE PERFORMANCE
│   │   │   ├── Query Shape
│   │   │   ├── Projection
│   │   │   ├── Tracking Cost
│   │   │   ├── Round Trips
│   │   │   └── Database Execution
│   │   │
│   │   ├── 47.43 N+1 QUERY PROBLEMS
│   │   │   ├── Lazy Loading
│   │   │   ├── Per-Row Queries
│   │   │   ├── Query Detection
│   │   │   ├── Eager Loading
│   │   │   └── Projection
│   │   │
│   │   ├── 47.44 CARTESIAN EXPLOSION
│   │   │   ├── Multiple Collections
│   │   │   ├── JOIN Multiplication
│   │   │   ├── Data Duplication
│   │   │   ├── Split Queries
│   │   │   └── Projection
│   │   │
│   │   ├── 47.45 QUERY PLAN ANALYSIS
│   │   │   ├── Generated SQL
│   │   │   ├── Execution Plan
│   │   │   ├── Index Usage
│   │   │   ├── Cardinality
│   │   │   └── Database Bottlenecks
│   │   │
│   │   ├── 47.46 DBCONTEXT POOLING ADVANCED
│   │   │   ├── Pool Reuse
│   │   │   ├── Tenant State
│   │   │   ├── Reset Behavior
│   │   │   ├── DI Interaction
│   │   │   └── Benchmarking
│   │   │
│   │   ├── 47.47 MODEL COMPILED OPTIMIZATION
│   │   │   ├── Compiled Models
│   │   │   ├── Model Initialization
│   │   │   ├── Generated Model Code
│   │   │   ├── Startup Performance
│   │   │   └── Large Models
│   │   │
│   │   ├── 47.48 EF CORE DIAGNOSTICS
│   │   │   ├── Logging
│   │   │   ├── DiagnosticSource
│   │   │   ├── Command Events
│   │   │   ├── Query Timing
│   │   │   └── SaveChanges Diagnostics
│   │   │
│   │   ├── 47.49 EF CORE TESTING
│   │   │   ├── Real Database Tests
│   │   │   ├── SQLite Tests
│   │   │   ├── Provider Differences
│   │   │   ├── Transaction Tests
│   │   │   └── Migration Tests
│   │   │
│   │   ├── 47.50 EF CORE PROVIDER DIFFERENCES
│   │   │   ├── SQL Translation
│   │   │   ├── Data Types
│   │   │   ├── Migrations
│   │   │   ├── Functions
│   │   │   └── Concurrency Semantics
│   │   │
│   │   ├── 47.51 EF CORE DATABASE DEPLOYMENT
│   │   │   ├── Migration Artifacts
│   │   │   ├── Deployment Ordering
│   │   │   ├── Application Compatibility
│   │   │   ├── Schema Verification
│   │   │   └── Rollback Strategy
│   │   │
│   │   └── 47.52 ADVANCED EF CORE PRACTICES
│   │       ├── Treat Migrations as Production Code
│   │       ├── Design Explicit Concurrency Policies
│   │       ├── Measure Before Applying Query Optimizations
│   │       ├── Inspect SQL and Database Plans
│   │       └── Preserve Compatibility During Schema Evolution
│   │
│   ├── 48. EF6
│   │   │
│   │   ├── 48.01 ENTITY FRAMEWORK 6 FOUNDATIONS
│   │   │   ├── ORM
│   │   │   ├── Entity Model
│   │   │   ├── DbContext
│   │   │   ├── LINQ to Entities
│   │   │   └── Database Providers
│   │   │
│   │   ├── 48.02 EF6 ARCHITECTURE
│   │   │   ├── Object Services
│   │   │   ├── Entity Client
│   │   │   ├── Metadata
│   │   │   ├── Provider Layer
│   │   │   └── Database
│   │   │
│   │   ├── 48.03 EF6 DBCONTEXT
│   │   │   ├── DbContext
│   │   │   ├── DbSet
│   │   │   ├── Configuration
│   │   │   ├── ChangeTracker
│   │   │   └── SaveChanges
│   │   │
│   │   ├── 48.04 EF6 DATABASE FIRST
│   │   │   ├── Existing Database
│   │   │   ├── EDMX
│   │   │   ├── Model Generation
│   │   │   ├── Entity Generation
│   │   │   └── Database Synchronization
│   │   │
│   │   ├── 48.05 EF6 MODEL FIRST
│   │   │   ├── Conceptual Model
│   │   │   ├── Designer
│   │   │   ├── Entity Definitions
│   │   │   ├── Relationships
│   │   │   └── Database Generation
│   │   │
│   │   ├── 48.06 EF6 CODE FIRST
│   │   │   ├── POCO Entities
│   │   │   ├── DbContext
│   │   │   ├── Conventions
│   │   │   ├── Data Annotations
│   │   │   └── Fluent API
│   │   │
│   │   ├── 48.07 EDMX
│   │   │   ├── Entity Data Model
│   │   │   ├── Conceptual Model
│   │   │   ├── Storage Model
│   │   │   ├── Mapping Model
│   │   │   └── Designer
│   │   │
│   │   ├── 48.08 EDMX CSDL
│   │   │   ├── Entity Types
│   │   │   ├── Properties
│   │   │   ├── Associations
│   │   │   ├── Entity Sets
│   │   │   └── Conceptual Schema
│   │   │
│   │   ├── 48.09 EDMX SSDL
│   │   │   ├── Database Tables
│   │   │   ├── Columns
│   │   │   ├── Keys
│   │   │   ├── Store Types
│   │   │   └── Storage Schema
│   │   │
│   │   ├── 48.10 EDMX MSL
│   │   │   ├── Entity Mapping
│   │   │   ├── Property Mapping
│   │   │   ├── Table Mapping
│   │   │   ├── Associations
│   │   │   └── Mapping Fragments
│   │   │
│   │   ├── 48.11 EF DESIGNER
│   │   │   ├── Visual Model
│   │   │   ├── Entities
│   │   │   ├── Associations
│   │   │   ├── Mapping Details
│   │   │   └── Model Browser
│   │   │
│   │   ├── 48.12 T4 CODE GENERATION
│   │   │   ├── T4 Templates
│   │   │   ├── Entity Generation
│   │   │   ├── Context Generation
│   │   │   ├── Template Customization
│   │   │   └── Regeneration
│   │   │
│   │   ├── 48.13 EF6 ENTITY MAPPING
│   │   │   ├── Tables
│   │   │   ├── Columns
│   │   │   ├── Keys
│   │   │   ├── Relationships
│   │   │   └── Inheritance
│   │   │
│   │   ├── 48.14 EF6 RELATIONSHIPS
│   │   │   ├── One-to-One
│   │   │   ├── One-to-Many
│   │   │   ├── Many-to-Many
│   │   │   ├── Foreign Keys
│   │   │   └── Navigation Properties
│   │   │
│   │   ├── 48.15 EF6 INHERITANCE
│   │   │   ├── TPH
│   │   │   ├── TPT
│   │   │   ├── TPC Concepts
│   │   │   ├── Discriminator
│   │   │   └── Mapping Trade-Offs
│   │   │
│   │   ├── 48.16 EF6 LINQ QUERIES
│   │   │   ├── IQueryable
│   │   │   ├── Where
│   │   │   ├── Select
│   │   │   ├── Ordering
│   │   │   └── Aggregation
│   │   │
│   │   ├── 48.17 EF6 LOADING STRATEGIES
│   │   │   ├── Eager Loading
│   │   │   ├── Lazy Loading
│   │   │   ├── Explicit Loading
│   │   │   ├── Include
│   │   │   └── Query Count
│   │   │
│   │   ├── 48.18 EF6 CHANGE TRACKING
│   │   │   ├── Entity States
│   │   │   ├── Original Values
│   │   │   ├── Current Values
│   │   │   ├── DetectChanges
│   │   │   └── SaveChanges
│   │   │
│   │   ├── 48.19 EF6 VALIDATION
│   │   │   ├── Entity Validation
│   │   │   ├── Data Annotations
│   │   │   ├── Validation Errors
│   │   │   ├── DbEntityValidationException
│   │   │   └── Business Validation
│   │   │
│   │   ├── 48.20 EF6 RAW SQL
│   │   │   ├── Database.SqlQuery
│   │   │   ├── DbSet.SqlQuery
│   │   │   ├── ExecuteSqlCommand
│   │   │   ├── Parameters
│   │   │   └── Result Mapping
│   │   │
│   │   ├── 48.21 EF6 STORED PROCEDURES
│   │   │   ├── Function Imports
│   │   │   ├── Stored Procedure Mapping
│   │   │   ├── Parameters
│   │   │   ├── Result Types
│   │   │   └── Modification Functions
│   │   │
│   │   ├── 48.22 EF6 TRANSACTIONS
│   │   │   ├── SaveChanges Transactions
│   │   │   ├── DbContextTransaction
│   │   │   ├── BeginTransaction
│   │   │   ├── TransactionScope
│   │   │   └── Existing Transactions
│   │   │
│   │   ├── 48.23 EF6 CONCURRENCY
│   │   │   ├── ConcurrencyCheck
│   │   │   ├── Timestamp
│   │   │   ├── Optimistic Concurrency
│   │   │   ├── DbUpdateConcurrencyException
│   │   │   └── Conflict Resolution
│   │   │
│   │   ├── 48.24 EF6 MIGRATIONS
│   │   │   ├── Enable-Migrations
│   │   │   ├── Add-Migration
│   │   │   ├── Update-Database
│   │   │   ├── Migration History
│   │   │   └── Migration Scripts
│   │   │
│   │   ├── 48.25 EF6 MIGRATION CONFIGURATION
│   │   │   ├── DbMigrationsConfiguration
│   │   │   ├── Automatic Migrations
│   │   │   ├── Seed
│   │   │   ├── Migration Directory
│   │   │   └── Context Key
│   │   │
│   │   ├── 48.26 EF6 DATABASE INITIALIZERS
│   │   │   ├── CreateDatabaseIfNotExists
│   │   │   ├── DropCreateDatabaseIfModelChanges
│   │   │   ├── DropCreateDatabaseAlways
│   │   │   ├── Custom Initializers
│   │   │   └── Initialization Strategy
│   │   │
│   │   ├── 48.27 EF6 INTERCEPTORS
│   │   │   ├── IDbCommandInterceptor
│   │   │   ├── Command Inspection
│   │   │   ├── Logging
│   │   │   ├── Timing
│   │   │   └── Cross-Cutting Behavior
│   │   │
│   │   ├── 48.28 EF6 ASYNC OPERATIONS
│   │   │   ├── ToListAsync
│   │   │   ├── FirstOrDefaultAsync
│   │   │   ├── SaveChangesAsync
│   │   │   ├── Async Queries
│   │   │   └── Cancellation
│   │   │
│   │   ├── 48.29 EF6 PERFORMANCE
│   │   │   ├── Query Compilation
│   │   │   ├── Tracking
│   │   │   ├── Lazy Loading
│   │   │   ├── Projection
│   │   │   └── Generated SQL
│   │   │
│   │   ├── 48.30 EF6 DATABASE LOGGING
│   │   │   ├── Database.Log
│   │   │   ├── SQL Output
│   │   │   ├── Parameters
│   │   │   ├── Query Duration
│   │   │   └── Diagnostics
│   │   │
│   │   ├── 48.31 EF6 TESTING
│   │   │   ├── Integration Tests
│   │   │   ├── Test Databases
│   │   │   ├── Context Tests
│   │   │   ├── Mapping Tests
│   │   │   └── Migration Tests
│   │   │
│   │   ├── 48.32 EF6 VS EF CORE
│   │   │   ├── Architecture
│   │   │   ├── Platform Support
│   │   │   ├── Feature Differences
│   │   │   ├── Provider Ecosystem
│   │   │   └── Migration Considerations
│   │   │
│   │   ├── 48.33 EF6 TO EF CORE MIGRATION
│   │   │   ├── Model Assessment
│   │   │   ├── API Differences
│   │   │   ├── Mapping Differences
│   │   │   ├── Query Differences
│   │   │   └── Incremental Migration
│   │   │
│   │   ├── 48.34 EDMX MODERNIZATION
│   │   │   ├── Existing EDMX
│   │   │   ├── Database Schema
│   │   │   ├── Reverse Engineering
│   │   │   ├── Fluent Configuration
│   │   │   └── Compatibility Verification
│   │   │
│   │   └── 48.35 EF6 ENGINEERING PRACTICES
│   │       ├── Understand Legacy Mapping Metadata
│   │       ├── Inspect Generated SQL
│   │       ├── Control Lazy Loading Deliberately
│   │       ├── Preserve Behavior During Modernization
│   │       └── Prefer Incremental Migration for Large Systems
│   │
│   └── 49. MICRO ORM & DATA LIBRARIES
│       │
│       ├── 49.01 MICRO ORM FOUNDATIONS
│       │   ├── SQL-First Data Access
│       │   ├── Object Mapping
│       │   ├── Lightweight Abstraction
│       │   ├── Explicit Queries
│       │   └── Minimal Change Tracking
│       │
│       ├── 49.02 MICRO ORM VS FULL ORM
│       │   ├── SQL Control
│       │   ├── Mapping Automation
│       │   ├── Change Tracking
│       │   ├── Productivity
│       │   └── Performance Trade-Offs
│       │
│       ├── 49.03 DAPPER FOUNDATIONS
│       │   ├── IDbConnection Extensions
│       │   ├── SQL Queries
│       │   ├── Parameters
│       │   ├── Object Mapping
│       │   └── Command Execution
│       │
│       ├── 49.04 DAPPER QUERY
│       │   ├── Query<T>
│       │   ├── QueryAsync<T>
│       │   ├── SQL Text
│       │   ├── Parameters
│       │   └── Result Enumeration
│       │
│       ├── 49.05 DAPPER SINGLE-ROW QUERIES
│       │   ├── QueryFirst
│       │   ├── QueryFirstOrDefault
│       │   ├── QuerySingle
│       │   ├── QuerySingleOrDefault
│       │   └── Result Semantics
│       │
│       ├── 49.06 DAPPER EXECUTE
│       │   ├── Execute
│       │   ├── ExecuteAsync
│       │   ├── INSERT
│       │   ├── UPDATE / DELETE
│       │   └── Rows Affected
│       │
│       ├── 49.07 DAPPER PARAMETERS
│       │   ├── Anonymous Objects
│       │   ├── DynamicParameters
│       │   ├── Input Parameters
│       │   ├── Output Parameters
│       │   └── Database Types
│       │
│       ├── 49.08 DAPPER PARAMETERIZATION
│       │   ├── SQL Injection Prevention
│       │   ├── Parameter Expansion
│       │   ├── IN Lists
│       │   ├── Null Values
│       │   └── Parameter Types
│       │
│       ├── 49.09 DAPPER TYPE MAPPING
│       │   ├── Column Names
│       │   ├── Property Names
│       │   ├── Constructors
│       │   ├── Custom Mapping
│       │   └── Type Handlers
│       │
│       ├── 49.10 DAPPER TYPE HANDLERS
│       │   ├── SqlMapper.TypeHandler
│       │   ├── SetValue
│       │   ├── Parse
│       │   ├── Custom Value Types
│       │   └── Handler Registration
│       │
│       ├── 49.11 DAPPER MULTI-MAPPING
│       │   ├── Joined Rows
│       │   ├── Multiple Object Types
│       │   ├── splitOn
│       │   ├── Mapping Delegate
│       │   └── Relationship Assembly
│       │
│       ├── 49.12 DAPPER QUERYMULTIPLE
│       │   ├── Multiple Result Sets
│       │   ├── GridReader
│       │   ├── Sequential Reading
│       │   ├── Multiple Models
│       │   └── Reduced Round Trips
│       │
│       ├── 49.13 DAPPER STORED PROCEDURES
│       │   ├── CommandType.StoredProcedure
│       │   ├── Input Parameters
│       │   ├── Output Parameters
│       │   ├── Return Values
│       │   └── Result Mapping
│       │
│       ├── 49.14 DAPPER TRANSACTIONS
│       │   ├── IDbTransaction
│       │   ├── BeginTransaction
│       │   ├── Command Transaction
│       │   ├── Commit
│       │   └── Rollback
│       │
│       ├── 49.15 DAPPER BUFFERING
│       │   ├── Buffered Results
│       │   ├── Unbuffered Results
│       │   ├── Memory Usage
│       │   ├── Connection Lifetime
│       │   └── Large Result Sets
│       │
│       ├── 49.16 DAPPER ASYNC DATA ACCESS
│       │   ├── QueryAsync
│       │   ├── ExecuteAsync
│       │   ├── Async Connections
│       │   ├── CommandDefinition
│       │   └── Cancellation
│       │
│       ├── 49.17 DAPPER COMMANDDEFINITION
│       │   ├── Command Text
│       │   ├── Parameters
│       │   ├── Transaction
│       │   ├── Timeout
│       │   └── CancellationToken
│       │
│       ├── 49.18 DAPPER SQL ORGANIZATION
│       │   ├── Inline SQL
│       │   ├── SQL Constants
│       │   ├── Query Objects
│       │   ├── SQL Files
│       │   └── Query Ownership
│       │
│       ├── 49.19 DAPPER CRUD PATTERNS
│       │   ├── Insert
│       │   ├── Select
│       │   ├── Update
│       │   ├── Delete
│       │   └── Generated Key Retrieval
│       │
│       ├── 49.20 DAPPER PAGINATION
│       │   ├── OFFSET Pagination
│       │   ├── Keyset Pagination
│       │   ├── Parameters
│       │   ├── Stable Ordering
│       │   └── Total Counts
│       │
│       ├── 49.21 DAPPER PERFORMANCE
│       │   ├── Mapping Overhead
│       │   ├── SQL Execution
│       │   ├── Round Trips
│       │   ├── Buffering
│       │   └── Allocation Cost
│       │
│       ├── 49.22 REPO DB FOUNDATIONS
│       │   ├── RepoDb
│       │   ├── Connection Extensions
│       │   ├── Mapping
│       │   ├── Query Operations
│       │   └── CRUD Operations
│       │
│       ├── 49.23 REPO DB QUERY OPERATIONS
│       │   ├── Query
│       │   ├── QueryAll
│       │   ├── QueryMultiple
│       │   ├── Expressions
│       │   └── Result Mapping
│       │
│       ├── 49.24 REPO DB CRUD
│       │   ├── Insert
│       │   ├── Update
│       │   ├── Delete
│       │   ├── Merge
│       │   └── Batch Operations
│       │
│       ├── 49.25 REPO DB BULK OPERATIONS
│       │   ├── BulkInsert
│       │   ├── BulkUpdate
│       │   ├── BulkDelete
│       │   ├── Batch Size
│       │   └── Provider Support
│       │
│       ├── 49.26 REPO DB MAPPING
│       │   ├── Class Mapping
│       │   ├── Property Mapping
│       │   ├── Attributes
│       │   ├── Fluent Mapping
│       │   └── Type Mapping
│       │
│       ├── 49.27 SERVICESTACK.ORMLITE FOUNDATIONS
│       │   ├── OrmLiteConnectionFactory
│       │   ├── Typed Models
│       │   ├── SQL Expressions
│       │   ├── CRUD APIs
│       │   └── Dialect Providers
│       │
│       ├── 49.28 ORMLITE CRUD
│       │   ├── Insert
│       │   ├── Select
│       │   ├── Update
│       │   ├── Delete
│       │   └── Save
│       │
│       ├── 49.29 ORMLITE SQL EXPRESSIONS
│       │   ├── From<T>
│       │   ├── Where
│       │   ├── Join
│       │   ├── OrderBy
│       │   └── Select
│       │
│       ├── 49.30 ORMLITE MAPPING
│       │   ├── Model Classes
│       │   ├── Attributes
│       │   ├── Table Names
│       │   ├── Column Names
│       │   └── Relationships
│       │
│       ├── 49.31 ORMLITE DIALECT PROVIDERS
│       │   ├── SQL Server
│       │   ├── PostgreSQL
│       │   ├── MySQL
│       │   ├── SQLite
│       │   └── Dialect Differences
│       │
│       ├── 49.32 ADO.NET EXTENSION LIBRARIES
│       │   ├── Connection Extensions
│       │   ├── Command Helpers
│       │   ├── Mapping Helpers
│       │   ├── Parameter Helpers
│       │   └── Transaction Helpers
│       │
│       ├── 49.33 CUSTOM DATA MAPPERS
│       │   ├── DbDataReader
│       │   ├── Column Mapping
│       │   ├── Object Construction
│       │   ├── Type Conversion
│       │   └── Null Handling
│       │
│       ├── 49.34 REFLECTION-BASED MAPPING
│       │   ├── Property Discovery
│       │   ├── Runtime Assignment
│       │   ├── Type Conversion
│       │   ├── Metadata Caching
│       │   └── Reflection Cost
│       │
│       ├── 49.35 COMPILED DATA MAPPERS
│       │   ├── Expression Trees
│       │   ├── Generated Delegates
│       │   ├── Cached Mapping
│       │   ├── Reduced Reflection
│       │   └── Mapping Performance
│       │
│       ├── 49.36 SOURCE-GENERATED DATA ACCESS
│       │   ├── Compile-Time Mapping
│       │   ├── Generated Commands
│       │   ├── Generated Materializers
│       │   ├── Native AOT
│       │   └── Runtime Overhead Reduction
│       │
│       ├── 49.37 MICRO ORM TRANSACTIONS
│       │   ├── DbTransaction
│       │   ├── Transaction Scope
│       │   ├── Multiple Commands
│       │   ├── Commit
│       │   └── Rollback
│       │
│       ├── 49.38 MICRO ORM CONNECTION MANAGEMENT
│       │   ├── DbConnection
│       │   ├── Connection Factory
│       │   ├── Connection Pooling
│       │   ├── Lifetime
│       │   └── Disposal
│       │
│       ├── 49.39 MICRO ORM QUERY DESIGN
│       │   ├── Explicit SQL
│       │   ├── Projection
│       │   ├── Joins
│       │   ├── Pagination
│       │   └── Query Ownership
│       │
│       ├── 49.40 MICRO ORM SECURITY
│       │   ├── Parameterized SQL
│       │   ├── Dynamic Identifiers
│       │   ├── Credential Security
│       │   ├── Least Privilege
│       │   └── Sensitive Data
│       │
│       ├── 49.41 MICRO ORM PERFORMANCE
│       │   ├── Query Performance
│       │   ├── Mapping Performance
│       │   ├── Round Trips
│       │   ├── Buffering
│       │   └── Connection Pooling
│       │
│       ├── 49.42 MICRO ORM DIAGNOSTICS
│       │   ├── SQL Logging
│       │   ├── Query Timing
│       │   ├── Parameter Inspection
│       │   ├── Database Errors
│       │   └── Correlation
│       │
│       ├── 49.43 MICRO ORM TESTING
│       │   ├── Integration Tests
│       │   ├── Query Tests
│       │   ├── Mapping Tests
│       │   ├── Transaction Tests
│       │   └── Provider Tests
│       │
│       ├── 49.44 EF CORE AND DAPPER HYBRID
│       │   ├── EF Core for Writes
│       │   ├── Dapper for Reads
│       │   ├── Shared Connections
│       │   ├── Shared Transactions
│       │   └── Explicit Boundaries
│       │
│       ├── 49.45 DATA ACCESS ABSTRACTIONS
│       │   ├── Query Services
│       │   ├── Repositories
│       │   ├── Data Gateways
│       │   ├── Command Handlers
│       │   └── Persistence Boundaries
│       │
│       ├── 49.46 REPOSITORY PATTERN TRADE-OFFS
│       │   ├── ORM Abstraction
│       │   ├── Query Flexibility
│       │   ├── Testability
│       │   ├── Leaky Abstractions
│       │   └── Domain Boundaries
│       │
│       ├── 49.47 UNIT OF WORK TRADE-OFFS
│       │   ├── Transaction Boundary
│       │   ├── DbContext
│       │   ├── Explicit Coordination
│       │   ├── Multiple Repositories
│       │   └── Redundant Abstraction
│       │
│       ├── 49.48 DATA ACCESS LIBRARY SELECTION
│       │   ├── Query Complexity
│       │   ├── SQL Control
│       │   ├── Change Tracking Needs
│       │   ├── Performance Requirements
│       │   └── Team Expertise
│       │
│       └── 49.49 MICRO ORM & DATA LIBRARY PRACTICES
│           ├── Keep SQL Explicit and Parameterized
│           ├── Measure Before Replacing an ORM
│           ├── Keep Transaction Ownership Clear
│           ├── Test Against the Real Database Engine
│           └── Choose Abstractions from Application Needs