# ACID in Relational Databases

ACID is an acronym for **Atomicity**, **Consistency**, **Isolation**, **Durability** – the four key properties that
guarantee reliable
transactions in relational databases. In practice, a transaction is a sequence of SQL statements that the database
executes as a single unit. The ACID rules
ensure that transactions leave the database in a valid state, even under concurrent load or in the face of failures.
Below we examine each property in depth, with a focus on PostgreSQL.

## Atomicity

**Definition**: Atomicity means a transaction’s operations all succeed or fail together. If any step in the transaction
fails (due to a crash, constraint violation, etc.), the entire transaction is rolled back, leaving the database state
unchanged. In other words, there are no “half-finished” transactions.

- In PostgreSQL, when you issue BEGIN; … COMMIT;, either all statements execute successfully, or none do. For example, a
  money transfer: If the second UPDATE fails (e.g. due to a CHECK or division by zero), PostgreSQL automatically rolls
  back the first one. No partial update remains.

```postgresql
-- BEGIN;
-- UPDATE accounts SET balance = balance - 100 WHERE id = 1;
-- UPDATE accounts SET balance = balance + 100 WHERE id = 2;
-- COMMIT;
```

- Internally, PostgreSQL uses **Write-Ahead Logging** (WAL) to make transactions atomic. Before marking a transaction as
  committed, it writes log records for every change and only acknowledges success after the log is safely flushed to
  disk. This ensures that even if the database crashes mid-commit, the recovery process can replay or undo all changes,
  preserving atomicity.
- **Savepoints**: You can also use savepoints to roll back part of a transaction. For example, SAVEPOINT sp1; … ROLLBACK
  TO
  sp1; lets you undo recent work without aborting the whole transaction. But if you ultimately ROLLBACK; the
  transaction, all changes (even before the savepoint) are undone.
- **Example (SQL)**: Suppose a transaction violates a foreign-key constraint:The second statement raises a foreign-key
  error. PostgreSQL aborts the transaction, rolls back the insert, and no row is added. This “all-or-nothing” behavior
  preserves database validity.

```postgresql
-- BEGIN;
--   INSERT INTO orders (id, customer_id, total) VALUES (1, 999, 500);  -- assume customer 999 doesn't exist
-- COMMIT;
```

## Consistency

**Definition**: Consistency means the database always remains in a valid state with respect to its rules and
constraints.
After a committed transaction, all integrity constraints (such as primary keys, foreign keys, CHECK constraints, NOT
NULL, unique indexes, etc.) must hold. If a transaction would violate any constraint at commit time, PostgreSQL forces
an automatic rollback

- **Database-enforced rules**: Consistency is not about concurrent access but about data validity. For example, if you
  have a table inventory(product_id PRIMARY KEY, stock CHECK (stock >= 0)), any transaction that tries to make stock
  negative will fail at commit. PostgreSQL ensures that updates never leave the database in a state violating these
  rules.
- **Transactional enforcement**: PostgreSQL allows temporary inconsistencies within a transaction (for example, you
  might
  delete a row that a subsequent statement in the same transaction refers to), but it does not let them survive the
  COMMIT. If any constraint is broken when you attempt to commit, PostgreSQL will abort the entire transaction.
- **Example (SQL)**: Consider two related tables with a foreign-key constraint:
  Even though this might run, at COMMIT PostgreSQL sees that orders.user_id = 42 has no matching user (since we deleted
  it). This violates the foreign-key constraint, so PostgreSQL rolls back the transaction. The database ends up as it
  started (with the user and without the new order), maintaining consistency.

```postgresql
-- BEGIN;
--   DELETE FROM users WHERE id = 42;
--   INSERT INTO orders (id, user_id, total) VALUES (101, 42, 300);
-- COMMIT;
```

- **Avoiding inconsistencies**: In application code, it’s important to handle constraint violations (e.g. catch
  exceptions, retry, or adjust logic) to avoid letting user code rely on inconsistent data. In practice, catching SQL
  exceptions or using ON CONFLICT clauses can help.

## Isolation

**Definition**: Isolation controls how and when the intermediate state of a transaction becomes visible to other
concurrent
transactions. PostgreSQL defines that the effects of a transaction are not visible to other transactions until it
commits. In other words, each transaction should run as if it were alone (to the degree specified by the isolation
level).
PostgreSQL (and the SQL standard) provides several isolation levels with different guarantees. In Postgres, you can set
the level per transaction, e.g.:

```postgresql
BEGIN;
SET TRANSACTION ISOLATION LEVEL REPEATABLE READ;
-- ... SQL statements ...
COMMIT;
```

The standard defines four levels, but PostgreSQL effectively has three distinct ones (it treats Read Uncommitted as Read
Committed internally). Below is a summary of each level and which anomalies it allows:

| Isolation Level              | Dirty Read         | Non-repeatable Read | Phantom Read                    | Serialization Anomaly |
|------------------------------|--------------------|---------------------|---------------------------------|-----------------------|
| **Read Uncommitted**         | Possible (allowed) | Possible            | Possible                        | Possible              |
| **Read Committed** (default) | Not possible       | Possible            | Possible                        | Possible              |
| **Repeatable Read**          | Not possible       | Not possible        | *(Postgres disallows phantoms)* | Possible              |
| **Serializable**             | Not possible       | Not possible        | Not possible                    | Not possible          |

- **Dirty Read**: A transaction reads data written by another uncommitted transaction. PostgreSQL never allows dirty
  reads;
  even in “READ UNCOMMITTED” mode, it behaves like Read Committed (you only see data from committed transactions).
- **Non-repeatable Read**: You read the same row twice and get different results because another transaction committed a
  change in between. This can occur in Read Committed, but is prevented in Repeatable Read and Serializable
- **Phantom Read**: You execute a query twice and the set of returned rows changes because another transaction inserted
  or deleted rows satisfying your query condition. In PostgreSQL, **Repeatable Read** (Postgres’ implementation) also
  avoids phantoms (contrary to the standard). Only in Serializable are phantoms strictly prohibited (and by spec, also
  in Serializable).
- **Serialization Anomaly**: The result of concurrent transactions cannot be reproduced by any serial order of those
  transactions. Only the Serializable level forbids this, by definition.

PostgreSQL implements Serializable using Serializable Snapshot Isolation (SSI). Under the hood, Postgres tracks
read/write dependencies and will abort (roll back) one of the transactions if it detects a dangerous overlap that could
cause a serialization anomaly . If you get an error like ERROR: could not
serialize access due to read/write dependencies, it means Postgres detected that two concurrent transactions couldn’t be
safely ordered, and one was aborted to preserve serializability. The
application should catch this SQL state (40001) and retry the transaction if needed.

- **MVCC and Isolation**: PostgreSQL uses Multi-Version Concurrency Control (MVCC) to provide these isolation guarantees
  efficiently. Each transaction sees a snapshot of the database at the start of the query (or transaction, depending on
  level), so readers do not block writers. Updates create new versions of rows, and old versions remain for transactions
  that need them. This allows high concurrency: for example, two transactions can update different rows of the same
  table without locking each other, and readers never block writers or vice versa.

```postgresql
-- Session 1 (T1), using default Read Committed:

-- BEGIN;
-- SELECT balance FROM accounts WHERE id = 1;  -- sees balance = 100
-- 
-- -- Meanwhile, Session 2 (T2):
-- BEGIN;
-- UPDATE accounts SET balance = balance + 50 WHERE id = 1;
-- COMMIT;
-- -- T2 has committed, balance is now 150 in the database.
-- 
-- -- Back to Session 1 (T1):
-- SELECT balance FROM accounts WHERE id = 1;  -- sees balance = 150 under Read Committed
-- COMMIT;
```

In **Read Committed**, the second SELECT in T1 sees the update from T2 (150). If T1 had been running at **Repeatable
Read** (snapshot isolation), it would have continued to see 100 in both selects, because its snapshot was taken at the
start of the transaction. This difference illustrates how higher isolation prevents non-repeatable reads but may require
T1 to retry if using serializable.

## Durability

**Definition**: Durability means that once a transaction commits, its changes survive permanently, even if the database
crashes or the power goes out. A durable system guarantees that “successfully committed” really means persistent.

- **WAL (Write-Ahead Log)**: PostgreSQL ensures durability through its Write-Ahead Logging mechanism. For every change,
  PG writes a WAL record describing the change. Crucially, this WAL record is flushed to disk before the transaction is
  reported as committed. Only after the flush does PG say “success”. Because the WAL is on disk, if the server crashes
  immediately after commit, recovery will replay the WAL and reapply the transaction changes, so no committed data is
  lost
- **Checkpoints and Buffer Cache**: After WAL, the actual data pages (tables/indexes) may remain in memory (dirty) for
  performance. Periodically, PostgreSQL runs a checkpoint where it writes all dirty pages to disk. The combination of
  WAL + checkpoints means the database can quickly recover to the most recent commit by replaying only the WAL changes
  since the last checkpoint.

```postgresql
-- BEGIN;
--   INSERT INTO orders (id, total) VALUES (101, 250);
-- COMMIT;

-- Assume crash happens here.
```

Because of durability, when PostgreSQL restarts, it replays the WAL and finds that the insert was committed. The row
with id=101 will be present after recovery. If WAL were not properly flushed, the insert might disappear.

- **Durability Settings**: By default, synchronous_commit is on, meaning commits wait for the WAL flush. In some
  high-throughput scenarios, DBAs may set synchronous_commit = off to gain speed at the risk of losing the last few
  transactions on a crash (trading durability for performance). However, most production systems leave it on for
  correctness.

## Real-World Considerations

In practice, achieving full ACID comes with engineering trade-offs. Below are common issues and how to handle them in
PostgreSQL.

- **Transaction Failures & Retries**: Serializable isolation or deadlocks can cause transactions to fail. For example,
  under
  **SERIALIZABLE**, Postgres may abort one of two conflicting transactions to avoid anomalies. The error SQLSTATE
  40001 (
  serialization_failure) indicates you should retry the transaction. Similarly, deadlock detection can abort a
  transaction (error 40P01). Best practice: Catch these exceptions in application code and retry the transaction after a
  short back-off. For Java/Spring, this typically means wrapping commits in a retry loop.
- **Deadlocks**: If two transactions each hold locks the other needs, PostgreSQL will detect the deadlock and abort one
  of
  them. For example, if T1 locks table A then B, and T2 locks B then A, neither can proceed. PostgreSQL will abort one (
  you’ll see an error). To prevent deadlocks, acquire locks in a consistent order and keep transactions short. If
  deadlocks do happen, catch the error and retry.
- **Lost Updates / Race Conditions**: In a high-concurrency environment, you may see “lost updates” if two transactions
  read-modify-write the same row. Example: T1 reads value=10, T2 reads value=10; T1 sets it to 15 and commits; T2 then
  sets it to 12 and commits—T1’s update is overwritten. Solutions include:
    - Use `SELECT ... FOR UPDATE` to lock the row explicitly. This causes T2 to wait until T1 commits, then T2’s read
      will
      see the updated value.
    - Use a higher isolation level (e.g. SERIALIZABLE) so that T2’s transaction is aborted if it conflicts.
    - Implement optimistic locking: add a version/timestamp column and check it on update (e.g.
      `WHERE id = ? AND version = ?`), so if it changed, the update fails and the app retries.
- **Transaction Timeouts**: Long-running transactions hold resources (locks, row versions) and increase conflict risk.
  It’s often wise to set a statement or lock timeout (SET LOCAL statement_timeout) so that runaway queries are killed
  rather than blocking others indefinitely. Also avoid “idle in transaction” sessions – any open transaction holds
  snapshot state and can bloat MVCC cleanup.
- **Isolation Level Tuning**: PostgreSQL’s default Read Committed is sufficient for many use cases and yields high
  concurrency. Use Repeatable Read or Serializable only if anomalies cannot be tolerated. Serializable provides the
  strongest guarantee but can reduce throughput under contention (due to more rollbacks on conflicts). Monitor
  pg_stat_database for “serialization failures” to see if you need to tune isolation levels or transaction logic.
  Sometimes “syntactic serializability” is enough: e.g., using SELECT FOR UPDATE or SERIALIZABLE only on critical
  sections, while letting other transactions run at Read Committed.
- **Locking Strategies**: PostgreSQL has several locking modes. Simple row locks (FOR UPDATE/FOR SHARE) can prevent many
  anomalies. For some cases, application-level advisory locks (pg_advisory_lock) can coordinate without touching tables.
  However, overusing locks can reduce concurrency. The system view pg_locks and the Deadlock errors can help diagnose
  which locks cause waits.

## ACID vs. Distributed and High-Performance Scenarios

Traditional ACID transactions are easiest to maintain on a single database node or small cluster. In very
high-throughput or distributed systems, strict ACID can become a bottleneck or even impossible (due to the CAP theorem,
a network partition forces a choice between consistency and availability. Engineers use various patterns to adapt:

- **Microservices & Sagas**: In a distributed architecture with multiple databases/services, a single ACID transaction
  across them is impractical. Instead, one can use a Saga pattern: a series of local transactions with compensating
  actions. For example, an order service and a payment service each update their own DB; if the payment fails, a
  compensating transaction in the order service rolls back the order. Sagas sacrifice global I (isolation) and A (
  atomicity across services) but allow eventual consistency. As Richardson notes, sagas lack isolation: developers must
  design carefully to avoid anomalies.
- **Eventual Consistency**: Some systems embrace BASE (Basically Available, Soft state, Eventual consistency) over ACID.
  In that model, updates propagate asynchronously (e.g. via message queues), and conflicts are resolved by merging or
  last-write-wins. This improves scalability and availability, but requires the application to tolerate temporary
  inconsistencies. For example, social media feeds often accept eventual consistency in exchange for high throughput.
- **Two-Phase Commit (2PC)** and Distributed Transactions: While PostgreSQL supports two-phase commit (PREPARE
  TRANSACTION / COMMIT PREPARED), it’s rarely used in microservices because it ties services together and is sensitive
  to failures. Instead, engineers often prefer idempotent retries and the Saga pattern as described. (If your
  architecture truly needs distributed ACID, distributed SQL databases like YugabyteDB or CockroachDB provide global
  transactions, but with complexity.)
- **Retries and Idempotency**: In any case, code that calls the database should be prepared to retry on transient
  errors (like deadlocks or serialization failures). Idempotent transaction design (where re-running a transaction has
  the same effect) makes retries safe. For example, use unique keys (ON CONFLICT DO NOTHING/UPDATE) or check conditions
  before inserts to avoid duplicate side-effects when retrying.
- **ACID and CAP**: Remember that ACID transactions generally prioritize consistency (C) over availability (A) in the
  face of a network partition. In a globally distributed setting, enforcing ACID often means sacrificing latency or
  availability. Systems like CockroachDB or Spanner use techniques (global clocks, Paxos/Raft) to keep ACID across
  regions, but many systems simply accept eventual consistency to stay responsive.

## Summary

ACID properties give relational databases like PostgreSQL a powerful guarantee: reliable, consistent state even with
concurrent users or failures. PostgreSQL’s MVCC and WAL architecture implement these properties efficiently. In code,
you manage transactions via BEGIN/COMMIT/ROLLBACK (or Connection.setAutoCommit(false) in Java). Use appropriate
isolation levels: the default Read Committed works for most cases, but consider Serializable (or explicit locking) if
you absolutely must avoid anomalies. Catch serialization or deadlock errors and retry.

In real-world systems, weigh the cost of strict ACID against performance and distribution needs. When full ACID is too
strict or cross-service consistency is required, engineers often use patterns like **sagas, compensating transactions,
and eventual consistency**. These give up some ACID guarantees (especially Isolation and Atomicity across services) to
gain scalability. Regardless, understanding ACID deeply – and how PostgreSQL enforces it – helps you design robust
transactional systems.

## Key takeaways:

- **Atomicity**: All-or-nothing execution of statements (Postgres rolls back on any failure)
- **Consistency**: Always respect constraints; invalid states are never committed
- **Isolation**: Control visibility among concurrent transactions (use SET TRANSACTION ISOLATION LEVEL; Postgres
  defaults to Read Committed)
- **Durability**: Committed changes survive crashes, thanks to WAL flushing before commit
- **Trade-offs**: Strict ACID may reduce throughput or availability. Distributed systems often use sagas or eventual
  consistency, accepting some anomalies
- **Practices**: Keep transactions short, handle errors (retry on serialization failures), and choose isolation levels
  wisely.