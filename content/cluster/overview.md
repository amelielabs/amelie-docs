---
weight: 1
title: "Overview"
bookToc: false
---

## Clustering

Amelie has a two-level architecture.

The **`first level`** implements a pool of workers (Frontend workers), each of which can handle a large
number of clients concurrently. It separates IO, HTTP, SQL parsing,
Bytecode compilation and distributed transaction execution coordination from actual data access and modification.
Increasing the worker's pool size allows the database to serve more clients and increases throughput.

The **`second level`** (Compute Nodes or Backend workers) handles actual data access and modification as
part of the globally distributed transaction driven by the session. A compute node is a special worker
thread designed to run in a tight loop with the Executor, sharing a single WAL.
Each node has an associated list of table partitions, which only this node can access individually without
interfering with other nodes.

Amelie supports non-interactive deterministic distributed multi-statement ACID transactions.
The Amelie executor executes distributed transactions in a deterministic order, implements **`GROUP COMMIT`**,
and manages write-ahead logging (WAL). All transactions always operate on a **`SERIALIZABLE`** level.

During initial repository creation, the number of compute nodes and frontend workers will be set automatically
according to the number of CPU cores in the system or configured manually. Compute nodes can also be created or
dropped in runtime using [CREATE NODE](/docs/cluster/create) or [DROP NODE](/docs/cluster/drop) commands.

The number of compute nodes and frontend workers is the primary factor that affects performance
(as well as WAL usage).

While having a distributed database design, Amelie currently does not support network nodes
(support for which will be added in the future releases). Only local compute nodes are supported.

In its current form, Amelie does not require the complex maintenance typical of distributed systems and
works as a single process, hiding all the complexity. Compute nodes do not require additional maintenance.
