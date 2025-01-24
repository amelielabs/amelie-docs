---
weight: 20
bookFlatSection: false
title: "Architecture"
bookToc: false
---

![image description](/docs/architecture/architecture.png)

## Architecture

Amelie has a unique two-level architecture for full parallelization, table partitioning, and lock-less execution.

It is based on the idea of automatically treating local machine CPU cores as if they were distributed system nodes,
sharding data, partitioning, and generating parallel group plans for all types of queries.

While having a distributed database design, it currently does not support network nodes
(this will be done in the future releases). In its current state, it does not require complex maintenance
typical to distributed systems and works as a single process, hiding all the complexity.

### Cooperative Multitasking

Amelie implements a custom asynchronous multi-threaded coroutine runtime. It handles all system OS aspects, such as networking and IPC.
Compared to the thread-per-connection approach, it allows for significantly scaling network throughput for short transactions.

One reason behind coroutine design is to make event-driven asynchronous applications look and feel like they were written in a
synchronous procedural manner instead of using the traditional callback approach.

### Frontend Workers

Amelie has a two-level architecture that separates IO, HTTP, SQL parsing,
Bytecode compilation, and distributed transaction execution coordination from actual data access and modification.

Frontend level implements a pool of workers each of which can handle a numerious number of clients concurrently.
This is implemented using cooperative multi-tasking (coroutines) and multi-threading.
By increasing the workers pool size it is possible to serve more clients in the database and
increase throughput.

### Backend Workers (Compute Nodes)

Compute nodes are responsible for handling actual data access and data modification as part of global distributed
transaction driven by the session (frontend).

Each node has an associated list of table partitions, which only this node can access individually without
interfering with other nodes. Each partition modification is done using the local transaction context.

Node executes incoming requests one by one in a strict order driven by the Executor.
Each request consists of a bytecode explicitly generated for this node to be executed by its virtual machine context.
Compute nodes can be created or dropped dynamicaly using [CREATE NODE](/docs/cluster/create) or [DROP NODE](/docs/cluster/drop).

### Bytecode Compiler

After being parsed, each SQL DML or Query statement generates two bytecode sections:

* The first one is for the distributed transaction coordination and results merging by the frontend session
* The second one is for the actual data access and modification for each node individually

```text {style="github-dark"}
explain select count(*) from test
[{
  "bytecode": {
    "coordinator": {
      "00": "send_all            0      0      -     # public.test",
      "01": "recv                0      0      0     ",
      "02": "merge_recv_agg      0      0      20    ",
      "03": "set                 1      1      0     ",
      "04": "store_open          1      0      6     ",
      "05": "jmp                 10     0      0     ",
      "06": "count               2      1      0     ",
      "07": "push                2      0      0     ",
      "08": "set_add             1      0      0     ",
      "09": "store_next          1      6      0     ",
      "10": "store_open          1      1      0     ",
      "11": "cte_set             0      1      0     ",
      "12": "content             0      -      -     ",
      "13": "ret                 0      0      0     "
    },
    "node": {
      "00": "set                 0      1      1     ",
      "01": "int                 1      -      0     # -2147483648",
      "02": "push                1      0      0     ",
      "03": "table_open          0      0      5     # public.test (primary)",
      "04": "jmp                 12     0      0     ",
      "05": "bool                1      1      0     ",
      "06": "push                1      0      0     ",
      "07": "set_get             1      0      0     ",
      "08": "int                 2      -      0     # 1",
      "09": "push                2      0      0     ",
      "10": "set_agg             0      1      20    ",
      "11": "table_next          0      5      0     ",
      "12": "table_close         0      0      0     ",
      "13": "bool                1      1      0     ",
      "14": "push                1      0      0     ",
      "15": "set_get             1      0      0     ",
      "16": "null                2      0      0     ",
      "17": "push                2      0      0     ",
      "18": "set_agg             0      1      20    ",
      "19": "result              0      0      0     ",
      "20": "ret                 0      0      0     "
    }
  }
}]
```

### Virtual Machine

A virtual machine interprets bytecode until completion and produces an accessible result.
The VM implementation uses an optimized register-based bytecode interpreter, similar to the spirit of one used in modern
programming languages.

Using this approach would allow to implement even more efficient JIT (Just-In-Time) compilation to machine
code in the future, using bytecode as an intermidient representation.

### Sharding

Amelie is using consistent hashing to assign each partition interval on table creation
(hash partitioning) and associate them with nodes. Some requests (like point-lookups) will be
executed only on one node, and others will need to be executed on several nodes.

### Deterministic Executor

Amelie follows a deterministic transactions approach (Calvin-style) for transaction processing since
it allows implementing a highly performant execution pipeline without dealing with complex distributed
snapshot issues and avoids multi-versioning (MVCC) altogether. It does not require periodic garbage collection and VACUUM.

The Amelie executor plays a crucial role in the system. It is responsible for executing distributed transactions
in a deterministic order, implementing Group Commit, and managing write-ahead logging (WAL).

The executor is optimized for pipelining and optimistic execution. New requests will not wait for the Commit event
for other ongoing transactions. Instead, the executor creates a dependency graph between transactions and
performs Group Abort in case of failure and Group Commit in the likely case of success. One session always becomes
Group Commit Leader to drive Group Commit logic.

All transactions always operate on a **`STRICT SERIALIZABLE`** level.

### DDL

DDL operations, such as [CREATE TABLE](/docs/sql/ddl/tables/create) or [DROP TABLE](/docs/sql/ddl/tables/drop), require an exclusive lock.
The lock is taken in coordination with other sessions first.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and [ALTER TABLE ADD COLUMN](/docs/sql/ddl/tables/alter) are
blocking but completely parallel. Each worker node will be involved in creating an index for its partitions.

### Distributed and Shared Tables

By default, all tables are **`distributed`**, meaning each table will have partitions created on each node
for parallel access or modification. It's important to note that currently, distributed tables cannot
be part of a JOIN with other distributed tables. However, they can be used as a part of a
multi-statement transaction or CTE.

To address this issue, we created a special type of table called **`shared`**. Those tables are not partitioned and
are available for direct read access from any node. They can be used to implement efficient parallel
JOIN operations with other distributed tables. However, frequent updating of a shared table is less
efficient since it requires coordination and exclusive access.

### Data Persistency

Amelie supports ACID transactions and Commits only if data is written to WAL first (unless it is configured not to do so).

The persistency model is based on classic In-Memory database logic using WAL with periodic Snapshotting.
[CHECKPOINT](/docs/reliability/checkpoint) operation is used to create data snapshot, it allows to scale this process by
running snapshot for each node individually in parallel. Checkpoint operation also is responsible for WAL retention.

During restart, the database finds and reads the latest snapshot files in parallel for each node individually,
reducing start time.

### Asynchronous Replication

Amelie supports Async Replication, which allows fault-tolerant Primary-Replica setups to be created.
This works by defining replicas on the Primary server using the [CREATE REPLICA](/docs/repl/create) statement.
Created replica objects are used to identify connecting servers, work as a replication slot to identify replica
position, and affect Primary server WAL garbage collection.

Replication is logical and based on WAL streaming. The replica must be created initially from the Primary
backup and up to date with its WALs.

### Protocol and Compatability

Amelie works over HTTP and does not require additional client libraries or compatibility with other databases.
Any modern programming language or tooling that supports HTTP and JSON can be used directly.

---
