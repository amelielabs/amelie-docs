---
weight: 1
title: Overview
type: docs
bookToc: false
---

## Transactions

Amelie supports non-interactive deterministic distributed multi-statement ACID transactions.
Non-interactive means that all transaction statements (including [BEGIN/COMMIT](/docs/sql/transactions/begin_commit))
must be provided for execution.

Amelie is designed for short ACID transactions and fast real-time analytics. It is not intended for
long, complex, multi-statement transactions or queries that generate large amounts of data.
There are configurable limits for transaction size.

Unless transaction is a basic expression or **`DDL`** command, it will be executed on
one or more nodes.

Transaction commits only if data is written to **`WAL`** first (unless it is configured not to do so).
In case of an error, the transaction will be automatically aborted on all nodes. An aborted transaction
might also abort other ongoing transactions that happen to be already processed (and not **`COMMITED`**) after
the aborted one (see Execution).

All transactions always operate on a **`STRICT SERIALIZABLE`** level.

### Processing

After being received and parsed, each transaction is compiled into two bytecode sections.

* The first one is for the distributed transaction coordination and results merging by the session
* The second one is for the actual data access and modification for each node individually

A **`Virtual Machine`** (VM) interprets bytecode until completion and produces an accessible result.
There are several VM contexts. One for each transaction coordinator and one for each compute node in the system.

Each session acts as a distributed transaction coordinator for compute nodes.

Amelie generates an optimized parallel plan for executing multi-statement transactions and [CTE](/docs/sql/transactions/cte).
It will combine together node requests to reduce wait times and speed up the execution of non-dependable CTE statements.

[EXPLAIN/PROFILE](/docs/sql/explain/) commands can be used to get more details about the transaction and its bytecode.

### Execution

The Amelie executor executes distributed transactions in a deterministic order, implements **`GROUP COMMIT`**,
and manages write-ahead logging (WAL).

A deterministic approach (Calvin-style) allows for the implementation of a highly performant execution
pipeline without dealing with complex distributed snapshot issues and avoiding multi-versioning.

The executor is optimized for fast, optimistic, lockless execution.

Transactions will not wait for the **`COMMIT`** event for other ongoing transactions. Instead, the executor creates
a dependency graph between transactions and performs **`GROUP ABORT`** in case of failure and **`GROUP COMMIT`** in the likely
case of success. One session always becomes the **`GROUP COMMIT Leader`** to drive the commit logic.

### DDL

Currently DDL commands cannot be part of a multi-statement transactions.

DDL operations, such as [CREATE](/docs/sql/ddl/tables/create) or [DROP TABLE](/docs/sql/ddl/tables/drop), require an exclusive lock.
The lock is taken in coordination with other sessions first.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and [ALTER TABLE ADD COLUMN](/docs/sql/ddl/tables/alter) are
blocking but completely parallel. Each node will be involved in creating an index for its partitions.

---
