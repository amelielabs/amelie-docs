---
weight: 1
title: "Overview"
bookToc: false
---

## Separate IO and Compute

Amelie has a two-level architecture.

The **`first level`** implements a pool of IO worker threads (Hosts), each of which can handle a large
number of clients concurrently. It separates IO, HTTP, SQL parsing,
Bytecode compilation and distributed transaction execution coordination from actual data access and modification.
Increasing the Hosts worker's pool size allows the database to serve more clients and increases throughput.

The **`second level`** (Compute Nodes) handles actual data access and modification as part of the distributed
transaction driven by the client session (initiated from one of the Host).
A compute node is a special worker thread designed to run in a tight loop with the Executor, sharing a single WAL.
Each compute node has an associated list of table partitions, which only this compute node can access individually
without interfering with other nodes.

Amelie supports non-interactive deterministic distributed multi-statement ACID transactions.
The Amelie executor executes distributed transactions in a deterministic order, implements **`GROUP COMMIT`**,
and manages write-ahead logging (WAL). All transactions always operate on a **`STRICT SERIALIZABLE`** level.

During initial repository creation, the number of compute nodes and hosts will be set automatically
according to the number of CPU cores in the system or configured manually. Compute nodes can also be created or
dropped dynamically using [ALTER COMPUTE](/docs/compute/alter) command.

The number of compute nodes and hosts is the primary factor that affects performance
(as well as WAL usage).

While having a distributed database design, Amelie currently does not support network compute nodes
(support for which will be added in the future releases).
Amelie does not require the complex maintenance typical of distributed systems and
works as a single process, hiding all the complexity.

Compute nodes do not require additional maintenance.

---
