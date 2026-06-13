---
weight: 2
title: Architecture
bookToc: true
---

![image description](/docs/compute/architecture.png)
### Our Vision
	
We believe the future belongs to real-time, intelligent systems — especially AI agents
that need to make fast decisions, coordinate with each other, react instantly,
maintain memory, and manage state reliably without conflicts.

Traditional relational databases were built for a different era.

Amelie was designed from the ground up as a high-performance, in-memory relational
database — purpose-built to serve as the backbone for modern real-time, data-intensive applications and AI agents.

It is engineered to operate on the frontline: acting as a fast, reliable operational database
that powers intelligent systems even under heavy contention and multi-tenancy.

### Project Goals

Our goal was to create a relational database that lives in the same world as classics
like PostgreSQL or MySQL — but bridges the gap between SQL and NoSQL, delivering competitive performance
with a modern alternative.

We revisited core architectural bottlenecks — lock contention, inefficient IO, and multi-versioning —
and built a system that does things differently for workloads with short, high-velocity transactions.

Amelie eliminates write-write conflicts entirely. Concurrent updates to the same keys never cause
aborts or rollbacks. This makes it exceptionally well-suited for high-volatility domains such as
Fintech, IoT (real-time device state), and dynamic AI agent systems.

It unifies ultra-fast OLTP, parallel vector search, instant table cloning, pub/sub, and
real-time event streaming — all in one in-memory relational database.

With easy access through HTTP APIs and native MCP support for both applications and AI agents.

### The CPU as Distributed Database

We built unique architecture for full parallelization and lockless transaction processing.
It treats local machine CPU cores as distributed system nodes, sharding, partitioning, and generating
parallel group plans for all queries.

While having a distributed database design, Amelie does not require the complex maintenance typical of distributed
systems and works as a single process, hiding all the complexity.

Amelie has two independent processing levels for IO and Compute — **`FRONTEND`** and **`BACKEND`** processing.

During initial repository creation, the number of frontend and backend workers will be set automatically
according to the number of CPU cores in the system or use some reasonable defaults.
Frontend and Backend workers can also be changed dynamically.

The number of worker is the primary factor that affects performance beside WAL.

### Distributed Transactions

Amelie supports non-interactive deterministic distributed multi-statement ACID transactions.
The Amelie executor executes distributed transactions in a deterministic order, implements **`GROUP COMMIT`**,
and manages write-ahead logging (WAL). All transactions always operate on a **`STRICT SERIALIZABLE`** level.

The current implementation does not support network-distributed transactions — all distributed transactions are local
and executed as part of the single process involving backend worker threads.

Transaction commits only if data is written to **`WAL`** first.
In case of an error, the transaction will be automatically aborted. An aborted transaction
might also abort other ongoing transactions that happen to be already processed (and not **`COMMITED`**) after
the aborted one. This is the only case when transaction can potentially get a conflict.

### Frontend Processing

The **`first processing level`** implements a pool of Frontend worker threads, each of which can handle many clients concurrently.
This is implemented using cooperative multitasking (coroutines) and multithreading.

It separates IO, HTTP/TLS, SQL parsing, Bytecode compilation, and distributed transaction execution coordination from
actual data access and modification.

Increasing the worker’s pool size allows the database to serve more clients and increases throughput.

### Cooperative Multitasking

Amelie implements a custom asynchronous multi-threaded coroutine runtime. It handles all system OS aspects,
including networking, IPC, and sessions.

Compared to the thread-per-connection approach, it significantly scales processing throughput for short
transactions by reducing the number of context switches for multiple connections, allowing more useful work.

### Backend Processing

The **`second processing level`** implements a pool of Backend worker threads.
It handles actual data access and modification as part of the distributed transaction driven by the client
session (initiated by one of the Frontend Workers).

A backend worker thread is designed to run in a tight loop with the Executor, sharing a single WAL.
Each worker has an associated list of table partitions, which it can access individually without
interfering with other workers. Each partition modification is done using the local transaction context.

The worker executes incoming requests in a strict order driven by the Executor. Each request consists of a
bytecode explicitly generated for this worker to be executed by its virtual machine context.

Backend workers can be created or dropped dynamically.

### Partitioning

All tables are partitioned (having at least 1 partition).
Partitions are created on each backend worker for parallel access or modification.

Partitions are implemented as dedicated **`Pods`** and work as coroutines with dedicated serial queues.
Backends workers host Pods. There is no strict association between the partitions (pods) and backends.
This enables independent dynamic scaling, moving, and rebalancing pods between backends.

### Heaps and Indexes

Partitions store rows in Heaps. **`Heap`** is a custom memory-allocator context designed for fast
in-memory usage and on-disk persistence. It has a shared-nothing design
(access by one partition at a time, with some exceptions). Designed for instant drop and disk write as a
large continuous memory blocks.

Amelie tables are Index-organized Tables (IOT). Tables always have a primary index. 
All indexes are built per partition and point directly to rows from the Heap. Secondary indexes
also point to the row, making them as fast as the primary index.

Tables can be directly joined with other tables and used in subqueries.
Amelie coordinates access to partitions created on other backends for those cases to avoid concurrent
writes simultaneously.

### Sharding

Consistent hashing is used to assign each partition interval on table creation (hash partitioning) and associate
them with backend workers. Some requests (like point-lookup DML) will be executed on one worker, and
others must be executed on several.

### Query Compiler

After being parsed, each transaction generates two bytecode sections:

* **`main`** — commands for the distributed transaction coordination and results processing by the frontend session.
* **`pushdown`** — commands for data access and modification on one or many backend workers (per partition).

```text
EXPLAIN SELECT data, count(*) FROM test GROUP BY data;

explain
───────

main
  0   send_all            0      0      40    # amelie.test (select, closing)
  1   recv_aggs           1      0      32
  2   set                 2      2      0
  3   store_open          3      1      10
  4   store_read          4      3      1
  5   push                4      0      0
  6   count               4      3      0
  7   push                4      0      0
  8   set_add             2      0      0
  9   store_next          3      4      0
 10   free                3      0      0
 11   free                1      0      0
 12   ret                 2      0      -

pushdown
  0   set                 0      1      1
  1   table_open          1      0      8     # amelie.test (primary) part
  2   table_readi32       2      1      -     # data
  3   push                2      0      0
  4   set_get             2      0      0
  5   push_int            -      0      0     # 1
  6   set_agg             0      2      32
  7   table_next          1      2      0
  8   free                1      0      0
  9   ret                 0      0      -

access
  •   amelie.test shared [select]
```

### Virtual Machine

A virtual machine interprets bytecode until completion and produces an accessible result.
The VM implementation uses an optimized register-based bytecode interpreter, similar to one used in
modern programming languages.

Using this approach would allow to implement even more efficient JIT (Just-In-Time) compilation to machine
code in the future, using bytecode as an intermidient representation.

### Deterministic Executor

Amelie follows a deterministic transaction processing approach.

It allows for implementing a highly performant execution pipeline without dealing with complex
distributed snapshot issues and avoids multi-versioning (MVCC) altogether. It does not require
periodic garbage collection and VACUUM.

The executor plays a crucial role in the system. It is responsible for executing distributed
transactions in a deterministic order, implementing **`GROUP COMMIT`**, and managing write-ahead
logging (WAL).

The **`GROUP COMMIT`** logic is separated into dedicated worker.

Each transaction either creates a new transaction group or matches an existing one by
analyzing overlapping partitions with other active transactions. This allows non-overlapping partitions on
the same backend workers to process and commit without locks,
while still maintaining serial execution access.

The executor is optimized for pipelining and optimistic execution. New requests will not wait
for the Commit event for other ongoing transactions. Instead, the executor creates a dependency
graph between transactions and performs Group Abort in case of failure and Group Commit in the
likely case of success.

### Transactions Without Conflicts

Due to the serial processing design, Amelie does not have transactional conflicts typical of MVCC systems.

All transactions always operate on a **`STRICT SERIALIZABLE`** level. This means that they always work and
own the latest, actual state of data.

Concurrent updates to the same keys never cause aborts, which is very beneficial in cases such as Fintech,
IoT (real-time state updates per device), or volatile AI-agentic systems.

### Reliability

Amelie supports ACID transactions and Commits only if data is written to WAL first (unless it is configured not to do so).

The persistency model is based on classic in-memory database logic using WAL and monotonically increasing
**`LSN`** (Log Sequence Number) with periodic snapshotting.

During restart, Amelie finds and reads the latest catalog file and replays WAL.
The catalog file keeps information about relations and partitions. All partitions are loaded in parallel
for each individually, reducing start time.

### Concurrency and Service

Amelie is not using `fork(2)` for CoW.

All snapshotting and service operations (such as index creation) are executed in multiple stages in
the background, allowing per-partition concurrency without locking ongoing transactions.

Catalog is decoupled from the actual checkpoint, which allows per-partition operations individually
to reduce memory usage and the system preasure.
