---
weight: 1
title: Overview
bookToc: false
---

## SQL

The SQL dialect is based on **`ANSI SQL`**, **`PostgreSQL`** and extended with unique features, such as
native JSON support and [Lambda aggregates](/docs/sql/query/lambda).

Amelie has a unique architecture for full parallelization and lockless transaction processing.
It treats local machine CPU cores as distributed system nodes, sharding, partitioning, and generating
parallel group plans for all queries.

Learn more about [How it Works](/docs/compute/overview).

### Transactions

Amelie supports non-interactive deterministic distributed multi-statement ACID transactions,
in which all transaction statements (including [BEGIN/COMMIT](/docs/sql/transactions/begin_commit))
must be provided for execution.

Amelie is designed for short ACID transactions and fast real-time analytics. It is not intended for
long, complex, multi-statement transactions or queries that generate large amounts of data.
There are configurable limits for transaction size.

Unless transaction is a basic expression or **`DDL`** command, it will be executed by
one or more backend workers.

All transactions always operate on a **`STRICT SERIALIZABLE`** level.

[EXPLAIN/PROFILE](/docs/sql/explain/) commands can be used to get more details about the transaction and its bytecode.

### Tables

All tables are **`PARTITIONED`** and distributed. Partitions will be created on each backend worker for
parallel access or modification.

Learn more about the [Partitioned Tables](/docs/sql/ddl/tables/create).

### DDL

Currently DDL commands cannot be part of a multi-statement transactions.

DDL operations, such as [CREATE](/docs/sql/ddl/tables/create) or [DROP TABLE](/docs/sql/ddl/tables/drop), require an exclusive lock.
The lock is taken in coordination with other sessions first.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and [ALTER TABLE ADD COLUMN](/docs/sql/ddl/tables/alter) are
blocking but completely parallel. Each backend worker will be involved in creating an index for its partitions.

### DML

The [INSERT / UPSERT](/docs/sql/dml/insert), [UPDATE](/docs/sql/dml/update) and [DELETE](/docs/sql/dml/delete) operations are distributed and will transactionally
update table partitions on one or more backends.

DML operations can be part of a multi-statement transaction.

### Select

The [SELECT](/docs/sql/query/select ) operation is distributed and transactional and will be executed on
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

### Lambda

Lambda is a unique construct that combines the functionality of a function and an
aggregate function with a state.
Lambda expressions can help work with JSON and do some non-trivial transformations.

Learn more about [Lambda](/docs/sql/query/lambda).

---
