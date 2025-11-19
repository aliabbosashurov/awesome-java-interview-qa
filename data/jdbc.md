# JDBC API

### 1.What is the JDBC API?

> JDBC (Java Database Connectivity) is a standard Java API for interacting with relational databases.

> It provides interfaces and classes to connect to databases, execute SQL queries, retrieve results, and manage
> transactions. JDBC abstracts database-specific implementations through drivers, enabling developers to write portable
> database code.

---

### 2.What is pgJDBC?

> pgJDBC is the official JDBC driver for PostgreSQL.

> It implements the JDBC interfaces (`Connection`, `Statement`, `ResultSet`) for PostgreSQL, translating JDBC calls into
> PostgreSQL wire protocol commands. It supports advanced features like SSL, server-side prepared statements, and
> PostgreSQL-specific data types (e.g., JSON, arrays, UUIDs).

---

### 3.What is the purpose of the DriverManager class?

> `DriverManager` manages database drivers and establishes connections.

> It maintains a registry of available JDBC drivers and selects the appropriate driver based on the JDBC URL.
`DriverManager.getConnection(url, user, password)` returns a `Connection` object. It supports automatic driver loading
> via SPI or explicit `Class.forName()`.

---

### 4.What is the purpose of the Connection interface?

> `Connection` represents a session with the database for executing SQL statements and managing transactions.

> It provides methods for creating `Statement`, `PreparedStatement`, `CallableStatement`, managing transactions (
`commit()`, `rollback()`), and configuring session settings (auto-commit, isolation level).

> A single `Connection` is not thread-safe; it should be used by one thread at a time. Modern applications use
> connection pooling (`DataSource`) to reuse `Connection` objects efficiently.

---

### 5.What is the purpose of the Statement interface?

> `Statement` is used to execute SQL queries against the database.

> It provides methods like `executeQuery()` for SELECT statements and `executeUpdate()` for INSERT, UPDATE, DELETE.
`Statement` supports both static SQL and batch execution. For parameterized queries, `PreparedStatement` is preferred.

> `Statement` is simple but vulnerable to SQL injection if used with string concatenation. `PreparedStatement` and
`CallableStatement` are safer and more efficient for repeated or parameterized queries.

---

### 6.What is the purpose of the PreparedStatement interface?

> `PreparedStatement` is used to execute parameterized SQL queries safely and efficiently.

> It allows SQL statements with placeholders (`?`) to be precompiled, improving performance for repeated executions.
> Parameters are set using type-safe methods like `setInt()`, `setString()`. It prevents SQL injection by separating SQL
> logic from input data.

> Prepared statements are precompiled by the database server, reducing parsing overhead. They also support batch
> execution for large-scale operations efficiently.

---

### 7.What is CallableStatement used for?

> `CallableStatement` is used to execute stored procedures in the database.

> It allows calling procedures and functions with input, output, and input/output parameters using
`{call procedureName(?,?)}` syntax. Parameters are registered and retrieved using `registerOutParameter()` and
`getXXX()` methods.

> Callable statements leverage database-side logic, reducing network round-trips and centralizing complex business rules
> within stored procedures.

---

### 8. What is a ResultSet and what are its main methods?

> `ResultSet` represents the data returned by executing a SQL query.

> It provides methods to iterate and access rows and columns, such as `next()`, `getInt()`, `getString()`,
`getObject()`. ResultSets can be scrollable, updatable, or read-only, and support metadata access via
`ResultSetMetaData`.

> `ResultSet` is tied to a `Statement` and connection; closing the `Statement` usually closes the `ResultSet`. Proper
> resource management is critical to prevent memory leaks.

---

### 9.What are the types of JDBC drivers? (Type 1, Type 2, Type 3, Type 4)

> JDBC drivers are classified by their architecture and translation approach:

- **Type 1:** JDBC-ODBC bridge
- **Type 2:** Native-API driver
- **Type 3:** Network protocol driver
- **Type 4:** Pure Java (thin) driver

- **Type 1:** Uses ODBC layer; platform-dependent; slow; obsolete.
- **Type 2:** Converts JDBC calls to database-specific native code; faster but requires client libraries.
- **Type 3:** Middleware translates JDBC calls into database-independent protocol; supports multiple DBs.
- **Type 4:** Directly converts JDBC calls into database-specific protocol; pure Java; widely used (e.g., pgJDBC).

---

### 10.What is a Connection Pool in JDBC and why is it needed?

> A Connection Pool is a reusable set of database connections to improve performance and resource management.
> Creating a database connection is expensive. A pool maintains a number of open connections ready for use. Applications
> borrow a connection, use it, and return it to the pool, reducing connection overhead and improving throughput.

> Connection pools also manage idle connection validation, max/min pool size, and timeout settings. Modern pools like
> HikariCP provide highly optimized implementations supporting multi-threaded environments efficiently.

---

### 11.What is the DataSource interface and how does it differ from DriverManager?

> `DataSource` provides a factory for database connections with advanced features like connection pooling, while
`DriverManager` provides basic connection management.

> `DataSource` is preferred in enterprise applications. It supports connection pooling, distributed transactions (XA),
> and JNDI lookup. `DriverManager.getConnection()` creates a new physical connection each time, while
`DataSource.getConnection()` can return pooled connections, improving performance.

> Using `DataSource` decouples application code from database configuration and allows container-managed transaction
> management, making it ideal for scalable, production-grade systems.

---

### 12.How are transactions managed in JDBC? (commit, rollback)

> Transactions in JDBC are managed via the `Connection` interface using `commit()` and `rollback()`.

- **Commit:** Persists all changes made during the transaction.
- **Rollback:** Reverts changes if an error occurs.  
  Transactions start when auto-commit is disabled (`setAutoCommit(false)`) and end with an explicit `commit()` or
  `rollback()`.

---

### 13.What is Auto Commit mode and how can it be disabled?

> Auto-commit mode automatically commits every SQL statement; it can be disabled via `connection.setAutoCommit(false)`.

- **Enabled (default):** Each statement is immediately committed.
- **Disabled:** Allows grouping multiple statements into a single transaction; developer must call `commit()` or
  `rollback()` manually.

---

### 14.What is the difference between PreparedStatement and Statement?

> `PreparedStatement` is precompiled and supports parameterized queries; `Statement` executes static SQL.

- **Statement:** Executes literal SQL; prone to SQL injection; cannot reuse precompiled SQL.
- **PreparedStatement:** Precompiles SQL, supports `?` placeholders, type-safe parameter binding, and batch execution;
  prevents SQL injection.

---

### 15.How to protect against SQL Injection attacks in JDBC?

**Short answer:**  
Use `PreparedStatement` with parameter binding instead of concatenating user input into SQL.

**Detailed explanation:**

- Avoid `Statement.execute("SELECT * FROM users WHERE id=" + userInput)`
- Use:

```java
//  PreparedStatement ps = conn.prepareStatement("SELECT * FROM users WHERE id = ?");
//  ps.setInt(1, userInput);
```

---

### 16. What are the differences between ResultSet types: TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, and TYPE_SCROLL_SENSITIVE?

- **TYPE_FORWARD_ONLY**: Cursor moves only forward; lightweight; cannot scroll.
- **TYPE_SCROLL_INSENSITIVE**: Cursor can scroll forward/backward; insensitive to database changes
  after query execution.
- **TYPE_SCROLL_SENSITIVE**: Cursor can scroll; reflects changes in the database after query
  execution.

---

### 17.What is ResultSet concurrency (CONCUR_READ_ONLY vs CONCUR_UPDATABLE)?

> ResultSet concurrency defines whether the ResultSet can be updated. `CONCUR_READ_ONLY` is read-only,
`CONCUR_UPDATABLE` allows updates.

- **CONCUR_READ_ONLY:** Default; no changes to the underlying database through the ResultSet.
- **CONCUR_UPDATABLE:** Allows using `updateXXX()`, `insertRow()`, and `deleteRow()` methods to modify the database
  directly from the ResultSet.

---

### 18. How is batch processing performed in JDBC?

> Batch processing allows executing multiple SQL statements in a single request for efficiency.

- Use `Statement.addBatch()` or `PreparedStatement.addBatch()` for multiple SQL statements.
- Execute all with `executeBatch()`.
- Reduces network round-trips and improves performance for bulk operations.

---

### 19.What is RowSet and how does it differ from ResultSet?

> `RowSet` is a disconnected, scrollable, and optionally serializable wrapper around a `ResultSet`.

- Implements `javax.sql.RowSet`.
- Can operate without an active database connection (disconnected).
- Supports event listeners, making it suitable for GUI applications or serialization.
- `ResultSet` is connected, tied to a `Statement` and `Connection`.

---

### 20.What new features were added in JDBC 4.0/4.1/4.2/4.3? (e.g., try-with-resources, auto-closing)

> JDBC 4.x introduced auto-loading drivers, try-with-resources support, new data types, and NIO support for large
> objects.

- **JDBC 4.0:** Auto-loading drivers via `META-INF/services`, `RowSet` improvements, annotations.
- **JDBC 4.1:** `Wrapper` and `unwrap()` enhancements, integration with `java.util.concurrent`.
- **JDBC 4.2:** Support for `java.time` API, `Connection#isValid()`.
- **JDBC 4.3:** Java 9+ compatibility, improved `Lob` streaming, enhanced `Connection` and `Statement` interfaces.
- **Try-with-resources:** `Connection`, `Statement`, `ResultSet` implement `AutoCloseable`.

---

### 21.How are BLOB and CLOB data types handled in JDBC?

> BLOB (Binary Large Object) and CLOB (Character Large Object) store large binary or character data and are handled via
> streaming APIs.

- **BLOB:** Use `getBlob()`, `setBlob()`, or `getBinaryStream()`/`setBinaryStream()`.
- **CLOB:** Use `getClob()`, `setClob()`, or `getCharacterStream()`/`setCharacterStream()`.
- Allows reading/writing large data incrementally to avoid memory overload.

---

### 22.

>
---

### 23.

>
---

### 24.

>
---

### 25.

>
---

### 26.

>
---

### 27.

>
---

### 28.

>
---

### 29.

>
---

### 30.

>
---

### 31.

>
---

### 32.

>
---

### 33.

>
---

### 34.

>
---

### 35.

>
---

### 36.

>
---

### 37.

>
---

### 38.

>
---

### 39.

>
---

### 40.

>
---

### 41.

>
---

### 42.

>
---

### 43.

>
---

### 44.

>
---

### 45.

>
---

### 46.

>
---

### 47.

>
---

### 48.

>
---

### 49.

>
---

### 50.

>
---

### 51.

>
---

### 52.

>
---

### 53.

>
---

### 54.

>
---

### 55.

>
---

### 56.

>
---

### 57.

>
---

### 58.

>
---

### 59.

>
---

### 60.

>
---

### 61.

>
---

### 62.

>
---

### 63.

>
---

### 64.

>
---

### 65.

>
---

### 66.

>
---

### 67.

>
---

### 68.

>
---

### 69.

>
---

### 70.

>
---

### 71.

>
---

### 72.

>
---

### 73.

>
---

### 74.

>
---

### 75.

>
---

### 76.

>
---

### 77.

>
---

### 78.

>
---

### 79.

>
---

### 80.

>
---

### 81.

>
---

### 82.

>
---

### 83.

>
---

### 84.

>
---

### 85.

>
---

### 86.

>
---

### 87.

>
---

### 88.

>
---

### 89.

>
---

### 90.

>
---

### 91.

>
---

### 92.

>
---

### 93.

>
---

### 94.

>
---

### 95.

>
---

### 96.

>
---

### 97.

>
---

### 98.

>
---

### 99.

>
---

### 100.

>
---