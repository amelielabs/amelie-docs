---
weight: 1
title: Overview
bookToc: true
---

# SQL Reference

### SQL

The SQL dialect is based on **`ANSI SQL`**, **`PostgreSQL`** and extended with unique features, such as
native JSON support and [Lambda aggregates](/docs/sql/ops/query/lambda).

Amelie has a unique architecture for full parallelization and lockless transaction processing.
It treats local machine CPU cores as distributed system nodes, sharding, partitioning, and generating
parallel group plans for all queries.

Learn more about [How it Works](/docs/db/architecture).

### Transactions

Amelie supports multi-statement ACID transactions,
in which all transaction statements (including [BEGIN/END](/docs/sql/transactions/begin_end))
must be provided for execution.

Amelie is designed for short ACID transactions. It is not intended for
long, complex, multi-statement transactions or queries that generate large amounts of data.
There are configurable limits for transaction size.

Unless transaction is a basic expression or **`DDL`** command, it will be executed on
one or more backend workers.

All transactions always operate on a **`STRICT SERIALIZABLE`** level.

[EXPLAIN/PROFILE](/docs/sql/ops/query/explain) commands can be used to get more details about the transaction and its bytecode.

### Tables

All tables are partitioned (having at least 1 partition).
Partitions are created on each backend worker for parallel access or modification.

Amelie tables are Index-organized Tables (IOT). Tables always have a primary index. 
All indexes are built per partition and point directly to rows from the Heap. Secondary indexes
also point to the row, making them as fast as the primary index.

Learn more about [Tables](/docs/sql/ddl/tables/create).

### Branches

Table branches can be [CREATED](/docs/sql/ddl/branches/create) based on tables or other branches. Branches are accessible as
dedicated relations with grants. All DML operations similar to the table are supported.

They can be used for temporary workloads or to organize multi-tenancy storage, where each user or
agent will use a branch instead of a new table.

Branches are applied instantly at the storage row/index level. Table indexes will automatically filter
rows based on the used branch.

Learn more about [Branches](/docs/sql/ddl/branches/create).

### Topics

Topics implement Pub/Sub queues. Unlike tables, topics do not have a schema (everything is converted to JSON) and
do not store data like tables do.

Instead, [PUBLISH](/docs/sql/ops/dml/publish) writes directly to the in-memory CDC queue and the WAL, which
allows the creation of a real-time communication layer for subscribers. Topics can be unlogged.

Topics are transactional and can be used in multi-statement transactions.

Learn more about [Topics](/docs/sql/ddl/topics/create).

### Subscriptions

Amelie supports persistent Subscriptions. They can be [CREATED](/docs/sql/ddl/subscriptions/create) any table or topic.
Subscription provides direct access to the CDC in-memory queue. Each subscription has a state based
on the WAL (**LSN**) position. Can be used for queries or real-time streaming.

The [ACKNOWLEDGE](/docs/sql/ops/acknowledge) command can be used to advance the position forward.

Learn more about [Subscriptions](/docs/sql/ddl/subscriptions/create).

### User-Defined Functions

User-defined Functions (UDFs) allow you to organize database operations using Functions.
They are stored in compiled form, providing a faster, more secure way to work with the database.

Functions can be used in [SELECT](/docs/sql/ops/query/select) expressions or called using the [EXECUTE](/docs/sql/ops/execute)
command or [HTTP/JSON-RPC API](/docs/api/overview).

Learn more about [Functions](/docs/sql/ddl/functions/create).

### DDL

Currently DDL commands cannot be part of a multi-statement transactions.

All DDL operations that modify catalog will require an exclusive catalog lock. The lock is taken in
coordination with other transactions.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and [ALTER TABLE ADD COLUMN](/docs/sql/ddl/tables/alter) are
non-blocking. Each backend worker will be involved in creating an index for its partitions incrementally and concurrently.

### DML

The [INSERT / UPSERT](/docs/sql/ops/dml/insert), [UPDATE](/docs/sql/ops/dml/update) and [DELETE](/docs/sql/ops/dml/delete) operations are distributed and will transactionally
update table partitions on one or more backends.

DML operations can be part of a multi-statement transaction.

### SELECT

The [SELECT](/docs/sql/ops/query/select) operation is distributed and transactional and will be executed on
one or more backends if tables are involved.

Operations such as **`GROUP BY`**, **`ORDER BY`** and **`JOIN`** will be executed individually per
backend in parallel. After the successful execution, the results of each computation are merged together,
processed, and returned.

### Native JSON Support

* JSON arrays and objects can be constructed without functions using the **`[]`**, **`{}`** operators
* JSON fields can be accessed directly without functions using the **`.`** and **`[`** operators
* JSON columns can store any JSON value (not only object) and is using memory efficient encoding
* Select expressions and subqueries can be executed natively inside JSON objects

Learn more about [JSON expressions](/docs/sql/expressions/json).

### Lambda Aggregates

Lambda is a unique construct that combines the functionality of a function and an
aggregate function with a state.
Lambda expressions can help work with JSON and do some non-trivial transformations.

Learn more about [Lambda Aggregates](/docs/sql/ops/query/lambda).

---
