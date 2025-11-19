# SQL (PostgreSQL based)

### 1.What is a database?

> A database is an organized collection of structured data stored electronically and accessed/controlled via a software
> system.
> A database provides persistent storage, indexing, crash recovery, concurrency control, and query processing. It
> abstracts physical storage details and offers a logical data model (relational, document, key-value, graph, etc.) that
> applications interact with.
---

### 2.What is DBMS?

> DBMS (Database Management System) is the software system that manages databases – storage engine, query processor,
> transaction manager, concurrency control, recovery system, etc.
> Examples: PostgreSQL, MySQL, Oracle, SQL Server (RDBMS); MongoDB, Cassandra, DynamoDB (NoSQL); Redis, Neo4j (
> specialized).
---

### 3.What types of DBMS exist?

> Relational (RDBMS), Key-Value, Document, Columnar, Graph, Time-Series, Wide-Column, In-Memory, NewSQL, Multi-model.

- **Relational DBMS** – table-based, SQL, ACID (PostgreSQL, Oracle)
- **Key-Value** – simple hash-like (Redis, DynamoDB)
- **Document** – JSON/BSON documents (MongoDB, CouchDB)
- **Wide-Column/Columnar** – column families (Cassandra, BigQuery, ClickHouse)
- **Graph** – nodes & relationships (Neo4j, ArangoDB)
- **Time-Series** – optimized for timestamped data (InfluxDB, TimescaleDB)
- **In-Memory** – DRAM-first (Redis, Memcached, SAP HANA)
- **NewSQL** – distributed SQL with horizontal scaling + ACID (CockroachDB, TiDB, YugabyteDB)
- **Multi-model** – supports several models in one engine (ArangoDB, Fauna)

---

### 4.What is RDBMS?

> Relational Database Management System – a DBMS that stores data in tables with rows and columns, enforces schema,
> primary/foreign keys, and follows the relational model (Codd, 1970).
> RDBMS implements the relational algebra, enforces referential integrity, provides declarative SQL, and guarantees ACID
> properties (usually via MVCC or locking).
---

### 5.What is the difference between DBMS and RDBMS?

> All RDBMS are DBMS, but not all DBMS are RDBMS. DBMS is the generic term; RDBMS is the subset that follows the
> relational model with tables, schemas and SQL.

> DBMS is any database management system (can be hierarchical, network, NoSQL, etc.).  
> RDBMS is a specific type of DBMS that strictly adheres to the relational model, enforces normalization, supports SQL,
> and provides strong consistency via transactions.
---

### 6.What is SQL?

> Structured Query Language — the ISO/ANSI standard declarative language for interacting with relational databases.
> It has sublanguages (DDL, DML, DQL, DCL, TCL) and is implemented by virtually every RDBMS with minor dialect
> differences.
> SQL is set-based and declarative: the optimizer decides execution order. Modern extensions include window functions,
> CTEs, JSON operators, generated columns, and full-text search.
---

### 7.What is a query?

> A client request expressed in SQL (or another query language) asking the DBMS to retrieve or modify data.
> The lifecycle: parse → rewrite → plan → optimize → execute → return results. Optimizer uses statistics, cardinality
> estimates, and cost models.
---

### 8.What are the elements of SQL?

- **DDL** – Data Definition Language (CREATE, ALTER, DROP, TRUNCATE)
- **DML** – Data Manipulation Language (INSERT, UPDATE, DELETE, MERGE)
- **DQL** – Data Query Language (SELECT)
- **DCL** – Data Control Language (GRANT, REVOKE)
- **TCL** – Transaction Control Language (COMMIT, ROLLBACK, SAVEPOINT, SET TRANSACTION)

---

### 9.What is DDL?

> Data Definition Language — SQL commands that define or modify database objects (tables, indexes, views, schemas,
> constraints).
> DDL is auto-committed in most RDBMS (cannot be rolled back in a transaction).
---

### 10.What is DML?

> Data Manipulation Language — SQL statements that insert, update, delete, or merge rows.
> DML is transactional and can be rolled back.
> High-performance DML pipelines use bulk loading (COPY, LOAD DATA), prepared statements, and batched upserts (ON
> CONFLICT / MERGE).
---

### 11.What is TCL?

> Transaction Control Language — commands that manage logical units of work (COMMIT, ROLLBACK, SAVEPOINT).
> PostgreSQL uses MVCC → no read locks, but long transactions bloat pg_xact and can cause vacuum issues. Oracle uses
> undo segments; SQL Server uses tempdb version store.
---

### 12.What is DQL?

> Data Query Language — typically just SELECT statements (often grouped under DML in practice).
> Modern DQL includes window functions (RANK, LAG), lateral joins, JSON/Table functions, and recursive CTEs — turning
> SQL
> into a full analytical language.
---

### 13.What clients do you know for PostgreSQL?

> psql, pgAdmin, DBeaver, DataGrip, TablePlus, Beekeeper Studio, and dozens of language drivers.

- **CLI:** psql (official), pgcli (autocompletion + syntax highlighting)
- **GUI:** pgAdmin 4 (web), DBeaver (universal), DataGrip (JetBrains), TablePlus (native), Beekeeper Studio (OSS),
  Postico (macOS)
- **Connection poolers / proxies:** PgBouncer, Odyssey, Heimdall
- **Drivers:** libpq (C), JDBC, Npgsql (.NET), psycopg3 (Python), pgx/pg (Go), rust-postgres
- **Web consoles:** Supabase Studio, Neon Console, Hasura (when backed by Postgres)
- **Migration / schema tools:** Flyway, Liquibase, Atlas, Bytebase

---

### 14.What is a table?

> A table is the fundamental data structure in a relational database — a collection of rows sharing the same set of
> typed columns, enforcing a strict schema.
> Each column has a name, data type, and optional constraints (NOT NULL, DEFAULT, etc.). Rows (tuples) are unordered
> unless an ORDER BY is applied. Physically, rows are stored in heap files (PostgreSQL), clustered indexes (SQL
> Server/InnoDB), or sorted by primary key (MySQL Cluster).
> In PostgreSQL, every table has a hidden tuple identifier (ctid), visibility info (xmin/xmax), and toast pointers for
> large values. Multiversion rows live in the heap until VACUUM removes dead tuples. Indexes are separate structures
> pointing to ctids.
---

### 15.What is upsert?

> Upsert (update-or-insert) is an atomic operation that inserts a row if it does not exist or updates it if a conflict (
> usually on primary key or unique constraint) occurs.

> Standard SQL: `INSERT ... ON CONFLICT [target] DO UPDATE SET ...` (PostgreSQL 9.5+, SQLite, modern MySQL with
`ON DUPLICATE KEY UPDATE`, SQL Server `MERGE`, Oracle `MERGE`).

> In PostgreSQL, `ON CONFLICT` uses inference from unique indexes/constraints to detect conflicts. The operation is
> fully transactional and ACID — either the insert or the update happens, never both, never neither. It avoids race
> conditions that two separate `SELECT → INSERT/UPDATE` statements would have.
---

### 16.What important commands do you know in psql?

**Meta-commands (always useful):**

- `\dt[+]` — list tables
- `\d+ name` — describe table + size + comments
- `\di[+]` — list indexes
- `\dv[+]` — list views
- `\ds[+]` — list sequences
- `\l+` — list databases with sizes
- `\du+` — list roles and privileges
- `\df+ function_name` — show function source
- `\timing` — toggle query timing
- `\watch 2` — re-run query every 2 seconds
- `\x auto` — expanded display for wide rows
- `\set AUTOCOMMIT off` — manual transaction control
- `\conninfo` — current connection details

**Power commands:**

- `\gexec` — execute the result of a query (dynamic SQL generation)
- `\sf+ function_name` — show function source code
- `\ef` — edit query/function in $EDITOR
- `\copy` — client-side fast CSV import/export (bypasses permission issues)
- `\c service=myservice` — switch connection using pg_service.conf

**Debugging / monitoring:**

- `\d config_file` → see postgresql.conf location
- `SELECT pg_stat_activity;` + `\d pg_stat_activity`
- `SELECT * FROM pg_stat_statements \watch 1`

---

### 17.What is a constraint?

> A constraint is a rule enforced by the RDBMS at the data level to guarantee integrity and correctness (NOT NULL,
> UNIQUE, PRIMARY KEY, FOREIGN KEY, CHECK, EXCLUDE).
> Constraints are stored in the system catalog and enforced on every DML operation. They can be deferrable, validated at
> commit time, and some support indexes (UNIQUE, PK, EXCLUDE).

- PRIMARY KEY → NOT NULL + UNIQUE with supporting index
- FOREIGN KEY → enforced via triggers or internal RI checks; can be NO ACTION, CASCADE, SET NULL, etc.
- CHECK → arbitrary boolean expression; PostgreSQL allows non-deterministic checks (but not recommended)
- EXCLUDE → generalized uniqueness (e.g., no overlapping time ranges using GiST)

---

### 18.What types of constraints exist in PostgreSQL?

> PostgreSQL supports six constraint types: NOT NULL, CHECK, UNIQUE, PRIMARY KEY, FOREIGN KEY, and EXCLUSION.
> All are defined at table level (or column level for simple ones) and stored in pg_constraint. They are enforced for
> every row modification unless explicitly marked DEFERRABLE/DEFERRED.

- NOT NULL and CHECK can be column constraints or table constraints
- UNIQUE and PRIMARY KEY automatically create a unique B-tree index
- FOREIGN KEY uses internal RI triggers + index on referencing columns for performance
- EXCLUSION constraints use GiST indexes and arbitrary operators (e.g., && for ranges, = for equality) — enabling rules
  like “no two bookings can overlap on the same room”

---

### 19.What is a foreign key constraint?

> A foreign key constraint enforces referential integrity: values in the referencing column(s) must exist in the
> referenced primary/unique key of another (or same) table.

---

### 20. What is a unique constraint?

> A unique constraint guarantees that no two rows in the table have the same values in the constrained column(s) (nulls
> are considered distinct).
> Can be column-level or table-level (partial, multi-column). Automatically backed by a unique B-tree index.

> PostgreSQL allows multiple NULLs in a UNIQUE column because NULL ≠ NULL in SQL semantics. Use UNIQUE NULLS NOT
> DISTINCT (PostgreSQL 15+) if you want standard SQL behavior (treat nulls as equal). Partial unique indexes (WHERE
> active = true) are extremely powerful for soft-delete patterns.
---

### 21. What is a check constraint?

> A check constraint enforces an arbitrary boolean expression on each row — if false, the insert/update is rejected.
> CHECK constraints are evaluated after BEFORE triggers but before AFTER triggers. They can reference other columns in
> the same row but not other rows. They are trusted by the optimizer for constraint_exclusion and index usage (e.g.,
> CHECK (country = 'US') enables partition pruning).

```sql
CHECK (price >= 0)  
CHECK (status IN ('active', 'inactive', 'archived'))  
CHECK (end_date >= start_date)
```

---

### 22. What is a not null constraint?

> A NOT NULL constraint forbids NULL values in a column — every row must have a non-null value.
> Can be declared inline (column_name text NOT NULL) or as a named table constraint. PostgreSQL stores nulls as bitmaps
> in
> the tuple header; NOT NULL columns save that bitmap space.
---

### 23.What is a primary key constraint?

> A primary key constraint is a combination of NOT NULL + UNIQUE on one or more columns and designates the official row
> identifier.
> Automatically creates a unique index (default B-tree). Only one PK per table. Most tables should have a surrogate
> bigint or uuid primary key.
---

### 24.What numeric data types exist in PostgreSQL?

| Type                   | Storage  | Range                                        | Use when                                             |
|------------------------|----------|----------------------------------------------|------------------------------------------------------|
| `smallint`             | 2 bytes  | –32 768 to +32 767                           | Tiny counters, status codes                          |
| `integer`              | 4 bytes  | –2.1B to +2.1B                               | Default integer choice, IDs < 2B                     |
| `bigint`               | 8 bytes  | –9 quintillion to +9 quintillion             | All modern primary keys, counters, snowflakes        |
| `numeric(p,s)`         | variable | Up to 131 072 digits before, 16 384 after .  | Finance, science, crypto balances — never use float  |
| `real` / `float4`      | 4 bytes  | ~6 decimal digits precision                  | Rarely — only when memory is extreme                 |
| `double precision`     | 8 bytes  | ~15 decimal digits precision                 | Scientific computing, ML features                    |
| `serial` / `bigserial` | —        | Auto-incrementing integer/bigint             | Legacy — prefer `GENERATED ALWAYS AS IDENTITY`       |
| `money`                | 8 bytes  | Currency with fixed 2-decimal locale display | Avoid — use `numeric(19,4)` + application formatting |

---

### 25.What is the difference between timestamp and timestamptz?

`timestamp without time zone` = absolute point in time stored naïvely (no TZ info)  
`timestamptz` (timestamp with time zone) = always stored internally as UTC and displayed in the session timezone
---

### 26.What ways exist to generate a UUID in PostgreSQL?

| Method                           | Extension | Version | Performance | Recommendation                               |
|----------------------------------|-----------|---------|-------------|----------------------------------------------|
| `gen_random_uuid()`              | pgcrypto  | v4      | Fastest     | Default choice since PostgreSQL 13           |
| `uuid_generate_v4()`             | uuid-ossp | v4      | Fast        | Legacy — still works, but requires extension |
| `uuid_generate_v1()` / `v1mc()`  | uuid-ossp | v1/v1mc | Medium      | Only if you need time+MAC ordering           |
| `gen_random_uuid()` + `uuid_nil` | pgcrypto  | —       | —           | Built-in constant for nil UUID               |

---

### 27. What is a sequence?

> A sequence is an independent database object that generates unique, auto-incrementing numeric values (usually for
> surrogate primary keys).

> Sequences are transaction-independent by default — nextval() is never rolled back (gaps are normal and expected).
> Use CACHE n for performance (pre-allocation).
> Modern replacement: GENERATED AS IDENTITY (see below).
---

### 28. What is "generated as identity"?

> Standard SQL way (PostgreSQL 10+) to create an auto-incrementing column backed by a sequence without manually creating
> one.

```sql
.
-- 
id bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY
-- or
id bigint GENERATED BY DEFAULT AS IDENTITY
-- 
CREATE TABLE users
(
    id         bigint GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    email      email NOT NULL UNIQUE,
    created_at timestamptz DEFAULT now()
);
```

---

### 29. What is a temp or temporary table?

> A temporary table exists only for the duration of the current session and is automatically dropped at session end.
---

### 30.What is a copy table?

> There is no dedicated “COPY TABLE” command in PostgreSQL.  
> “Copy table” is informal engineer-speak for duplicating a table’s structure and/or data using one of several idiomatic
> patterns.

| Goal                                                                               | Command (2025 best practice)                                                                                        | What you get                                         | When to use                                      |
|------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------|------------------------------------------------------|--------------------------------------------------|
| 1. Exact clone (structure + constraints + constraints + indexes + defaults + data) | ```sql\nCREATE TABLE users_backup (LIKE users INCLUDING ALL);\nINSERT INTO users_backup SELECT * FROM users;\n```   | Perfect 1:1 copy including PK, FK, indexes, comments | Backup before dangerous migration, testing       |
| 2. Structure only (full schema clone)                                              | ```sql\nCREATE TABLE users_v2 (LIKE users INCLUDING ALL);\n```                                                      | Empty table with all constraints, indexes, defaults  | Zero-downtime schema changes, new version tables |
| 3. Data + structure, no constraints                                                | ```sql\nCREATE TABLE users_new AS SELECT * FROM users;\n``` or\n```sql\nCREATE TABLE users_new AS TABLE users;\n``` | Data + column types + defaults, but no PK/FK/indexes | Quick analytics, staging, ad-hoc copies          |
| 4. Minimal structure only                                                          | ```sql\nCREATE TABLE users_new (LIKE users INCLUDING DEFAULTS INCLUDING CONSTRAINTS);\n```                          | Only column definitions + NOT NULL + CHECK           | When you will add your own PK/indexes afterward  |

---

### 31.What is a column alias?

> A column alias is a temporary name given to a column or expression in the SELECT list, visible in the result set and
> usable in ORDER BY / HAVING of the same query.

```sql
SELECT price * quantity                      AS total,
       price * quantity                         line_total, -- AS optional
       upper(first_name || ' ' || last_name) AS "Full Name" -- quotes only when needed
FROM orders;
```

---

### 32. Explain the ORDER BY clause

> ORDER BY sorts the final result set by one or more expressions in ascending (ASC, default) or descending (DESC) order,
> with explicit NULLS FIRST/LAST handling.

```sql
ORDER BY created_at DESC NULLS LAST
ORDER BY country ASC, revenue DESC
ORDER BY 3                                          -- positional (3rd column in SELECT)
ORDER BY salary * 1.1 DESC                          -- any expression
ORDER BY status = 'active' DESC, name ASC           -- boolean-first pattern (active rows first)
ORDER BY created_at DESC COLLATE "C"                -- fastest byte-order sort
```

---

### 33. What is DISTINCT?

> DISTINCT removes duplicate rows from the result set (based on all selected columns or specific expressions).

```sql
SELECT DISTINCT user_id
FROM orders; -- unique users
SELECT DISTINCT
ON (user_id) user_id, created_at -- keep first row per user
FROM orders
ORDER BY user_id, created_at DESC;
```

---

### 34. What is the purpose of the BETWEEN operator?

> BETWEEN is syntactic sugar for an inclusive range test: x BETWEEN a AND b ≡ x >= a AND x <= b.

```sql
WHERE created_at BETWEEN '2025-01-01' AND '2025-01-31'
WHERE price BETWEEN 10 AND 100
WHERE status BETWEEN 'A' AND 'M'                       -- lexicographic range
```

---

### 35.What is the difference between LIKE and ILIKE operators?

LIKE is case-sensitive pattern matching.  
ILIKE is case-insensitive pattern matching (PostgreSQL-specific).

```sql
WHERE name LIKE 'john%'     -- matches john, johnny, but NOT John
WHERE name ILIKE 'john%'    -- matches john, John, JOHN, JoHnNy
```

---

### 36. What are the purposes of ALL, ANY, and EXISTS, and in which situations are they used?

```postgresql
-- ALL
WHERE salary > ALL (SELECT salary FROM legacy_employees)   -- greater than the highest

-- ANY / SOME (identical semantics)
WHERE salary > ANY (SELECT salary FROM managers)          -- greater than at least one
WHERE department = ANY('{sales,marketing,support}')       -- IN replacement for arrays

-- EXISTS (most important in practice)
WHERE EXISTS (SELECT 1 FROM orders o WHERE o.user_id = users.id)  -- has orders?
```

---

### 37.What is the purpose of the CONCAT_WS function?

> CONCAT_WS (concat with separator) concatenates strings with a separator, skipping NULLs.

```sql
CONCAT_WS
(', ', 'John', 'Doe', NULL, 'Jr')
→ 'John, Doe, Jr'
CONCAT_WS(' | ', first_name, last_name, title)
→ safe full name even if title NULL
```

---

### 38. What is the purpose of the TO_DATE function, and how does it work?

```sql
TO_DATE
('2025-01-15', 'YYYY-MM-DD')
→ 2025-01-15 (date)
TO_DATE('15/01/2025', 'DD/MM/YYYY')
→ 2025-01-15
TO_DATE('Jan 15 2025', 'Mon DD YYYY')
→ 2025-01-15
```

---

### 39.What is the purpose of SIMILAR TO ?

> SIMILAR TO is SQL-standard regular expression matching (LIKE + regex features).

```sql
WHERE phone SIMILAR TO '%$$ (\d{3}) $$ \d{3}-\d{4}'   -- matches (123) 456-7890
WHERE email SIMILAR TO '%@%.%'                      -- very basic validation
```

---

### 40. What is the purpose of POSIX regular expressions?

```sql
WHERE name   ~ '^J.*n$'          -- starts with J, ends with n
WHERE name  ~* '^J.*n$'         -- case-sensitive
WHERE name  ~* '^j.*n$'          -- case-insensitive (preferred)
WHERE email ~* '^[A-Z0-9._%+-]+@[A-Z0-9.-]+\.[A-Z]{2,}$'  -- proper email regex
```

---

### 41.When is the GROUP BY statement used (why is it needed)?

> GROUP BY is required whenever a query mixes non-aggregated columns with aggregate functions (COUNT, SUM, AVG, etc.) in
> the same SELECT list.
> Without GROUP BY, the database wouldn’t know how to combine rows into groups before applying aggregates.  
> Example: “Give me total sales per country” → rows must be grouped by country first.
---

### 42. What is the syntax of the GROUP BY statement?

```postgresql
GROUP BY country, city                                      -- classic
GROUP BY user_id                                            -- most common
GROUP BY date_trunc('month', created_at)                    -- functional grouping
GROUP BY ROLLUP(country, region, city)                      -- subtotals + grand total
GROUP BY CUBE(status, source, date_trunc('day', created_at)) -- all combinations
GROUP BY GROUPING SETS ((country), (status), ())            -- multiple groupings in one query
```

---

### 43.When is the HAVING clause used?

> HAVING filters groups after aggregation — it is the WHERE clause for grouped data.
---

### 44. What is the syntax of the HAVING clause?

```postgresql
-- HAVING __boolean-condition__
HAVING count(*) >= 5
HAVING sum(amount) > 1000000
HAVING max(created_at) < '2025-01-01'
HAVING count(*) FILTER (WHERE active) > 10     -- PostgreSQL-specific
HAVING string_agg(name, ', ') LIKE '%Admin%'
```

---

### 45. What is the difference between the HAVING clause and the WHERE clause?

- **WHERE** filters rows before grouping and aggregation
- **HAVING** filters groups after grouping and aggregation

---

### 46. What is the purpose of the UNION statement, and why is it used?

> UNION combines result sets from multiple SELECTs into a single result set, removing duplicates (UNION ALL keeps them).

```postgresql

SELECT id, name
FROM users_2024
UNION ALL
SELECT id, name
FROM users_2025
ORDER BY name;
-- ORDER BY only at the very end

-- With explicit column list for safety
    (SELECT id, name, '2024' AS source FROM users_2024)
    UNION ALL
    (SELECT id, name, '2025' AS source FROM users_2025)
    ORDER BY source DESC, name;
```

---

### 47.What is the INTERSECT statement?

> INTERSECT returns only the rows that appear in both SELECT result sets (set intersection with automatic duplicate
> removal).

```sql
SELECT user_id
FROM customers
INTERSECT
SELECT user_id
FROM subscribers;
-- Returns users who are both customers AND subscribers
```

---

### 48. What is the syntax of the INTERSECT statement?

```sql
SELECT...FROM...
    INTERSECT [ALL]
SELECT...FROM...
    [
ORDER BY...]
```

```sql
SELECT id
FROM events_2024
INTERSECT ALL
SELECT id
FROM events_2025
ORDER BY id;
```

---

### 49. What is the EXCEPT statement?

> EXCEPT returns rows that appear in the first query but NOT in the second (set difference, duplicates removed).

```sql
SELECT user_id
FROM customers
EXCEPT
SELECT user_id
FROM banned_users;
-- All customers except banned ones
```

---

### 50. What is the syntax of the EXCEPT statement?

```sql
SELECT...FROM...
    EXCEPT [ALL]
SELECT...
    [
ORDER BY...]
```

```postgresql
SELECT email
FROM users_old
EXCEPT ALL
SELECT email
FROM users_new; -- emails deleted in new version
```

---

### 51.What is a view?

> A view is a named, stored SELECT query that behaves like a virtual table — you query it with SELECT, but no data is
> stored.
---

### 52.What is a virtual table?

> "Virtual table" is another name for a standard (non-materialized) view.
> It exists only as a definition in the catalog (pg_class with relkind = 'v'). Every time you query it, PostgreSQL
> rewrites and executes the underlying SELECT.
---

### 53.How does a standard view work?

> The view definition is stored and substituted into the query at parse time (query rewrite phase).

```postgresql
CREATE VIEW active_users AS
SELECT *
FROM users
WHERE status = 'active'
  AND deleted_at IS NULL;

SELECT *
FROM active_users
WHERE country = 'US';
-- Becomes internally:
SELECT *
FROM users
WHERE status = 'active'
  AND deleted_at IS NULL
  AND country = 'US';
```

---

### 54.What is a materialized view?

> A materialized view is a view whose result is physically stored on disk (like a table) for performance.
> Use when the underlying query is expensive (aggregations, joins across large tables) and data can be slightly stale.
---

### 55.How does a materialized view work?

> Data is pre-computed and stored in a real physical table. Queries against the matview are fast (no recomputation), but
> data is not automatically up to date.
---

### 56. How can data in a materialized view be refreshed?

```postgresql
-- First time + unique index for CONCURRENTLY
CREATE MATERIALIZED VIEW daily_sales AS
SELECT date_trunc('day', created_at) ::date AS day,
       sum(amount)                          AS revenue
FROM orders
GROUP BY 1;

CREATE UNIQUE INDEX ON daily_sales (day);

-- Daily refresh without blocking reads
REFRESH
    MATERIALIZED VIEW CONCURRENTLY daily_sales;
```

---

### 57.What is PL/pgSQL?

> PL/pgSQL is PostgreSQL’s native procedural language — a strongly-typed, SQL-embedded language for writing functions,
> procedures, triggers, and control logic directly inside the database.
> It supports variables, conditionals (IF/ELSE), loops (FOR, WHILE, LOOP), exception handling (BEGIN … EXCEPTION),
> cursors, dynamic SQL (EXECUTE), and RETURN.
---

### 58.Why should PL/pgSQL be used?

| Reason                             | Real-world impact                                                                |
|------------------------------------|----------------------------------------------------------------------------------|
| Atomic multi-statement logic       | One function = one transaction if called alone → perfect for business operations |
| Performance (query plan caching)   | First 5–10 executions after create/invalidate are cached → huge speedup          |
| Security (no client round-trips)   | Sensitive logic never leaves the DB, no SQL injection via app string concat      |
| Triggers & constraints on steroids | Complex validation, audit trails, soft deletes, denormalization                  |
| Data consistency                   | Guarantees the same logic runs everywhere (app, cron, migration, manual fix)     |
| Can call from any client           | Same function works from Python, Go, Node, psql, cron — single source of truth   |

---

### 59.What is a dollar-quoted string constant?

> Dollar-quoting is PostgreSQL’s escape-free way to write string literals (especially useful for multi-line SQL inside
> functions).
> No need to double single quotes. The tag (anything between $and$) just has to match. Common
> tags: $sql$, $body$, $function$, $json$.

```sql
$$
SELECT *
FROM users
WHERE id = $1 $$
-- or with tag
$func$INSERT
INTO logs
VALUES ('error', $1)$$ func $$
```

---

### 60.What is an anonymous block?

> An anonymous block (DO block) is an unnamed PL/pgSQL snippet executed once, directly from psql or client.

```postgresql
DO
$$
    DECLARE
        rec record;
    BEGIN
        FOR rec IN SELECT id, email FROM users WHERE inactive
            LOOP
                PERFORM send_deletion_email(rec.email);
                DELETE FROM users WHERE id = rec.id;
            END LOOP;
    END
$$;
```

---

### 61. What is a rowtype variable?

```postgresql
-- DECLARE
--     user_row users%ROWTYPE;           -- all columns of users table
-- order_row orders%ROWTYPE;
-- BEGIN
-- SELECT * INTO user_row FROM users WHERE id = 42;
-- RAISE NOTICE 'Email: %', user_row.email;
-- END;
```

---

### 62.What is a record variable?

**Short answer:**  
A `RECORD` variable is a generic row-type variable that can hold a row of any table or query result (dynamically typed
at runtime).

**Detailed explanation:**

```postgresql
-- DECLARE
--     r RECORD;                          -- can hold any row
-- BEGIN
-- FOR r IN SELECT * FROM users WHERE active LOOP
--         RAISE NOTICE 'User: % (%)', r.id, r.email;
-- END LOOP;
-- END;
```

---

### 63.How can variables be made constant?

> Add the CONSTANT keyword — value is assigned at declare time and cannot be changed afterward.

```postgresql
DECLARE
    batch_size CONSTANT int := 1000;
cutoff_date    CONSTANT timestamptz := '2025-01-01'::timestamptz;
tax_rate       CONSTANT numeric := 0.21;
BEGIN
    -- batch_size := 5000;   -- ERROR: cannot assign to constant
END;
```

---

### 64. What is the syntax of the IF statement?

```postgresql
-- IF condition THEN
--     statements;
-- ELSIF condition THEN
--     statements;
-- ELSE
--     statements;
-- END IF;
-- 
-- -- Example
-- IF v_count = 0 THEN
--     RAISE NOTICE 'No rows found';
-- ELSIF v_count BETWEEN 1 AND 100 THEN
-- PERFORM process_small_batch();
-- ELSE
-- PERFORM process_large_batch(v_count);
-- END IF;
```

---

### 65. What is the syntax of the CASE statement?

```postgresql
CASE expression
    WHEN value1 THEN result1
    WHEN value2 THEN result2
    ELSE default_result
END

-- Example
    status_text := CASE status
    WHEN 'active'   THEN 'Running'
    WHEN 'paused'   THEN 'Stopped'
    ELSE 'Unknown'
END;
```

```postgresql
CASE
    WHEN amount > 1000000 THEN 'whale'
    WHEN amount > 10000   THEN 'dolphin'
    WHEN amount IS NULL   THEN 'unknown'
    ELSE 'regular'
END
```

---

### 66.What ways exist to create loops in PL/pgSQL?

**Short answer:**  
PL/pgSQL supports four loop constructs:

1. Unconditional `LOOP` (with `EXIT`)
2. `WHILE` loop
3. Integer `FOR` loop (range)
4. Query `FOR` loop (over result set) — the most widely used in production.

**Detailed explanation & Final Version (2025 best practice with examples):**

```postgresql
-- 1. Basic LOOP (infinite until EXIT)
-- LOOP
--     -- do work
--     EXIT WHEN v_counter >= 1000;
--     v_counter := v_counter + 1;
-- END LOOP;
-- 
-- -- 2. WHILE loop
-- WHILE v_remaining > 0 LOOP
--     PERFORM process_batch(1000);
--     SELECT count(*) INTO v_remaining FROM queue WHERE processed = false;
-- END LOOP;
-- 
-- -- 3. Integer FOR loop (forward or reverse)
-- FOR i IN 1..1000 LOOP
--     PERFORM cleanup_old_data(i);
-- END LOOP;
-- 
-- FOR i IN REVERSE 2024..2020 BY 2 LOOP
--     RAISE NOTICE 'Year: %', i;
-- END LOOP;
-- 
-- -- 4. Query FOR loop (by far the most common in real code)
-- FOR rec IN
--     SELECT id, email, balance
--     FROM users
--     WHERE balance < 0
--     ORDER BY created_at
-- LOOP
--     PERFORM send_overdue_notice(rec.email);
--     UPDATE users SET overdue_notified = true WHERE id = rec.id;
-- END LOOP;
-- 
-- -- With explicit target type (recommended)
-- FOR rec users%ROWTYPE IN
--     SELECT * FROM users WHERE inactive
-- LOOP
--     PERFORM archive_user(rec);
-- END LOOP;
```

---

### 67.What is the purpose and syntax of the RAISE statement?

> `RAISE` emits log messages or throws exceptions from PL/pgSQL code.

````postgresql
RAISE [level] 'message string' [, variable];
RAISE [level] 'message % %', var1, var2;
RAISE SQLSTATE '22012' USING MESSAGE = 'Division by zero', DETAIL = '…';
RAISE EXCEPTION 'User % not found', user_id
      USING ERRCODE = 'foreign_key_violation';
````

---

### 68.How many levels exist in the RAISE statement?

> 6 levels: DEBUG, LOG, INFO, NOTICE, WARNING, EXCEPTION.
---

### 69.What is the default level in the RAISE statement?

> NOTICE (if no level is specified).
---

### 70. How is exception handling performed in PL/pgSQL?

```postgresql
-- BEGIN
-- -- normal code
-- EXCEPTION
--     WHEN division_by_zero THEN
--         RAISE NOTICE 'Caught division by zero';
-- RETURN 0;
-- WHEN unique_violation THEN
--         RAISE NOTICE 'Duplicate key – skipping';
-- WHEN OTHERS THEN
--         RAISE;   -- re-raise original exception
-- END;
```

---

### 71. What is a function?

> A function is a stored PL/pgSQL (or other language) routine that returns a value (scalar, table, void, etc.) and can
> be used in SQL statements.
---

### 72.What is a procedure?

> A procedure (introduced in PostgreSQL 11) is a stored routine that does not return a value directly and is executed
> with CALL.

```postgresql
CALL reindex_large_tables();
CALL migrate_user_data(2025);
```

---

### 73. What are the differences between IN, OUT, and INOUT parameters?

| Mode  | Direction      | Default | Typical use                                    |
|-------|----------------|---------|------------------------------------------------|
| IN    | Input only     | Default | Normal parameters (read-only inside function)  |
| OUT   | Output only    | —       | Return multiple values without `RETURNS TABLE` |
| INOUT | Input + output | —       | Pass value in, get modified value back         |

```postgresql
CREATE FUNCTION calc_tax(price IN numeric, tax_rate IN numeric DEFAULT 0.21, total OUT numeric)
    RETURNS numeric AS
$$
BEGIN
    total := price * (1 + tax_rate);
    RETURN total;
END;
$$ LANGUAGE plpgsql;
```

---

### 74. How can a function return a table?

```postgresql
CREATE OR REPLACE FUNCTION active_users(min_balance numeric DEFAULT 0)
    RETURNS TABLE
            (
                id      bigint,
                email   text,
                balance numeric
            )
AS
$$
BEGIN
    RETURN QUERY
        SELECT u.id, u.email, u.balance
        FROM users u
        WHERE u.active
          AND u.balance >= min_balance;
END;
$$ LANGUAGE plpgsql;
```

```postgresql
-- CREATE FUNCTION recent_orders(user_id bigint)
--     RETURNS SETOF orders AS $$
-- SELECT * FROM orders WHERE customer_id = user_id ORDER BY created_at DESC LIMIT 50;
-- $$ LANGUAGE sql;
```

---

### 75.What is a trigger?

> A trigger is a special function that is automatically executed in response to INSERT, UPDATE, DELETE, or TRUNCATE on a
> table.

```postgresql
CREATE TRIGGER users_audit_trg
    BEFORE INSERT OR UPDATE
    ON users
    FOR EACH ROW
EXECUTE FUNCTION audit_user_changes();

-- Trigger function must return TRIGGER
CREATE FUNCTION audit_user_changes() RETURNS trigger AS
$$
BEGIN
    IF TG_OP = 'UPDATE' AND NEW.email <> OLD.email THEN
        INSERT INTO user_email_history(user_id, old_email, new_email, changed_at)
        VALUES (NEW.id, OLD.email, NEW.email, now());
    END IF;
    RETURN NEW; -- or NULL for BEFORE triggers that reject
END;
$$ LANGUAGE plpgsql;
```

> Key variables inside trigger functions:
> NEW, OLD, TG_TABLE_NAME, TG_OP, TG_WHEN (BEFORE/AFTER), TG_LEVEL (ROW/STATEMENT)
---

### 76.What is the concept of a ROLE in PostgreSQL?

> A ROLE is the only security principal in PostgreSQL — it can represent a user (login role) or a group (non-login
> role).

> PostgreSQL unified users and groups into roles (since 8.1).  
> Every database connection is performed as a role.  
> Roles can own objects, have privileges, and be members of other roles.

Key role attributes:

- `LOGIN` → can connect (a “user”)
- `NOLOGIN` → cannot connect (a “group”)
- `SUPERUSER`, `CREATEDB`, `CREATEROLE`, `REPLICATION`, `BYPASSRLS`, etc.

---

### 77. What is the syntax for creating a role?

```postgresql
CREATE ROLE name [ [NO]LOGIN ]
    [ PASSWORD 'password' | DISABLE ]
    [ VALID UNTIL 'timestamp' ]
    [ IN ROLE role_name | IN GROUP role_name ]
    [ ROLE role_name [, ...] ]     -- grant membership
    [ CONNECTION LIMIT n ]
    [ BYPASSRLS | NOBYPASSRLS ]
    [ CREATEDB | NOCREATEDB ]
    [ SUPERUSER | NOSUPERUSER ];
```

```postgresql
-- Application user
CREATE ROLE myapp_user LOGIN PASSWORD 'strong-pwd-2025' CONNECTION LIMIT 50;

-- Group role
CREATE ROLE analytics_team NOLOGIN;

-- Service account with least privilege
CREATE ROLE reporting_user LOGIN PASSWORD '...' INHERIT;
GRANT analytics_team TO reporting_user;
```

---

### 78.What is the purpose of GRANT?

> GRANT gives a role specific privileges on database objects (tables, schemas, functions) or role membership.

```postgresql
GRANT SELECT, INSERT, UPDATE ON ALL TABLES IN SCHEMA public TO app_user;
GRANT USAGE, SELECT ON ALL SEQUENCES IN SCHEMA public TO app_user;
GRANT EXECUTE ON FUNCTION process_payment(numeric) TO api_user;
GRANT analytics_team TO john_doe; -- make john member of analytics_team
GRANT pg_read_all_data TO monitoring; -- built-in predefined role
```

---

### 79. What is the purpose of REVOKE?

```postgresql
REVOKE INSERT, UPDATE, DELETE ON ALL TABLES IN SCHEMA public FROM app_user;
REVOKE analytics_team FROM john_doe;
REVOKE ALL ON SCHEMA sensitive FROM public; -- remove default public access
```

```postgresql
REVOKE ALL ON DATABASE mydb FROM public;
REVOKE ALL ON SCHEMA public FROM public;
ALTER DEFAULT PRIVILEGES REVOKE EXECUTE ON FUNCTIONS FROM public;
```

---

### 80.What is a tablespace?

> A tablespace is a physical storage location (directory on disk) where PostgreSQL stores database objects (tables,
> indexes, matviews).
> pg_default (same as data directory), pg_global (shared objects).
---

### 81. How can a custom tablespace be created?

```postgresql
-- 1. Create directory on server (as OS user postgres)
sudo mkdir /ssd_tablespace
sudo chown postgres:postgres /ssd_tablespace

-- 2. Create tablespace
CREATE TABLESPACE fast_ssd LOCATION '/ssd_tablespace';

-- 3. Use it
CREATE TABLE metrics_2025
(
    ...)
    TABLESPACE
    fast_ssd;
CREATE INDEX CONCURRENTLY ON orders (created_at) TABLESPACE fast_ssd;

-- Move existing object
ALTER TABLE huge_table
    SET TABLESPACE fast_ssd;
```

```postgresql
CREATE TABLESPACE nvme_data LOCATION '/nvme/pg_data';
CREATE TABLESPACE hdd_archive LOCATION '/hdd/pg_archive';
```

---

### 82.What is a schema?

> A schema is a logical namespace inside a database that contains tables, views, functions, types, etc.

- One database → many schemas (public, analytics, staging, tenant_123, etc.)
- Schemas control object naming and search_path
- Fully independent privilege model

```postgresql
CREATE SCHEMA analytics;
CREATE SCHEMA tenant_42 AUTHORIZATION tenant_42_app;

-- Multi-tenant
SET search_path = tenant_42, public;
SELECT *
FROM customers;
-- resolves to tenant_42.customers

-- Clean separation
GRANT USAGE ON SCHEMA analytics TO analyst_role;
GRANT ALL ON ALL TABLES IN SCHEMA analytics TO analyst_role;
```

---

### 83. What is ACID?

Look: [What is ACID?](acid.md)

---

### 85. What is a transaction?

> A transaction is an atomic sequence of database operations executed as a single logical unit.
> A transaction ensures ACID properties—Atomicity, Consistency, Isolation, Durability. Either all operations succeed and
> commit, or none apply. It protects data from partial updates, concurrency issues, and failures.

---

### 86.What is the purpose of a rollback?

> Rollback reverses all uncommitted operations in a transaction.
> Rollback aborts the current transaction and restores the database to its state at the transaction’s start. It is used
> when an error, constraint violation, or business-rule failure occurs.

---

### 87.What is the purpose of a savepoint?

> A savepoint allows partial rollback inside a transaction.
> Savepoints create a checkpoint so you can rollback to that point without aborting the entire transaction. Useful for
> complex workflows where some steps may fail but the transaction should continue.

---

### 88.What does it mean to join a table?

> Joining means combining two tables based on a related key.
> A join creates a result set using matching conditions (typically key–foreign-key). The join type defines how matching
> and non-matching rows are handled.

---

### 89.How many types of joins are there in PostgreSQL?

> PostgreSQL supports INNER, LEFT, RIGHT, FULL, CROSS, and NATURAL joins.
> Core relational joins:

- INNER JOIN
- LEFT OUTER JOIN
- RIGHT OUTER JOIN
- FULL OUTER JOIN
- CROSS JOIN
- NATURAL JOIN

> Additionally:

- SELF JOIN (conceptual)
- LATERAL JOIN (advanced dependent-subquery join)

---

### 90.What is a natural join?

> A natural join automatically joins tables using all columns with matching names.
> It implicitly matches columns with the same names and returns each column once. While concise, it can be risky because
> schema changes may alter join behavior.

---

### 91.What is an index used for?

> An index accelerates data lookups by avoiding full table scans.
> It stores sorted or hashed references to rows, enabling fast search, filtering, and join operations. Indexes reduce
> I/O but increase write overhead due to maintenance on inserts/updates/deletes.

---

### 92.What is the difference between a unique index and a regular index?

> A unique index enforces value uniqueness; a regular index does not.

> Unique indexes guarantee no duplicate values in the indexed column(s). Regular indexes only optimize lookup but allow
> duplicates. PostgreSQL enforces uniqueness during writes by checking index entries before committing.

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