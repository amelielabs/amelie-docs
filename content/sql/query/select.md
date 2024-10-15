---
weight: 1
title: "SELECT"
bookToc: false
---

## SELECT Statement

```SQL
SELECT [DISTINCT] expr[, ...]
[INTO cte]
[[FROM [schema.]object_name | cte | expr[, ...]
 [JOIN [schema.]object_name | cte | expr ON (expr) [, ...]]
 [USE INDEX (name)]]
[GROUP BY expr[, ...]]
[WHERE expr]
[ORDER BY [ASC|DESC] expr[, ...]]
[LIMIT expr] [OFFSET expr]
```

Retrieve rows from a table, view, CTE, array, or object.

If the object schema is not defined, the object will be searched in the **`public`** schema.

Select operation is distributed and transactional and will be executed on one or more nodes if tables are
involved. Amelie is designed to split the work between partitions and compute nodes (**`PUSHDOWN`**).

Operations such as **`GROUP BY`**, **`ORDER BY`**, partial aggregations, and **`JOIN`** will be executed individually per
compute node in parallel. After the successful execution, the results of each computation are merged together,
processed, and returned.

It is possible to join tables, views, CTE, arrays, and objects together. Currently, only **`INNER JOIN`** is supported and
will be extended in future releases. Joining distributed tables directly has some limitations.

Select can be part of a multi-statement transaction and executed inside expressions (as subquery).

Amelie generates an optimized parallel plan for executing multi-statement transactions and CTE. It combines node
requests (pipeline) to reduce wait times and speed up the execution of non-dependable CTE statements.

Amelie is designed for short ACID transactions and fast real-time analytics. It is not intended for long, complex,
multi-statement transactions or queries that generate large amounts of data. There are configurable limits for
transaction size.

The **`INTO`** clause provides an alternative way to define the statement as a CTE.

### Index and Keys matching

By default, Amelie will try to use the most suitable index by matching keys by analyzing the **`WHERE`** expression.
It tries to identify whether the operation requires a **`range scan`** (start, stop conditions) or **`point lookup`** (by key).
This logic applies to the **`UPDATE`** and **`DELETE`** operations as well.

It is possible to force a query to use a specific index by using the **`USE INDEX`** clause for each table target. Primary index
keys are used for partitioning, where the primary or secondary index can be used by compute nodes for data scan
inside partitions.

### Distributed JOIN and Shared Tables

By default, all tables are **`distributed`**, meaning each distributed table will have partitions created on each node
for parallel access or modification. Currently, distributed tables cannot be used directly in a **`JOIN`** with other
distributed tables. However, they can be used in a multi-statement transaction or CTE.

There is also a particular type of table called **`shared`**. Those tables have only one partition and are available for
direct read access from any node. They can be used to implement efficient parallel **`JOIN`** operations with other
distributed tables. Frequent updating of a shared table is inefficient since it requires coordination and exclusive access.

### Subqueries

Currently, subqueries can be made to shared tables, views, and expressions only. Subqueries to other distributed tables
are not supported directly. Instead, CTE must be used. It will guarantee that a query to the distributed table is
executed only once and not nested.

---

```SQL
select {"at": current_timestamp, "id": system.config().uuid}
[{
  "at": "2024-09-26 16:14:00.722393+03",
  "id": "a74fbf39-cc9d-314e-a33e-3aa47559ffe5"
}]

select {"list": select * from [1,2,3]}
[{
  "list": [1, 2, 3]
}]
```

```SQL
-- distributed JOIN using shared dictionary table
create table collection(id int primary key)
create shared table dict(id int primary key) with (type = 'hash')

insert into dict values (1), (3)
insert into collection values (1), (2), (3)

select c.* from collection c join dict on (dict.id = c.id)
[[1], [3]]
```

```SQL
-- distributed JOIN using CTE
create table t1 (id int primary key)
create table t2 (id int primary key)

insert into t1 values (1), (3)
insert into t2 values (1), (2), (3)

with t1_result (id) as (
    select * from t1
) select t2.* from t2 join t1_result on (t2.id = t1_result.id)
[[1], [3]]
```

```SQL
select now()
["2024-09-29 10:56:52.753882+03"]

select *, count(*)
from generate_series(now() - interval '1 hour', now() - interval '1 min', interval '1 min')
group by date_bin(interval '15 minutes', *, now() - interval '1 hour')
order by *;
[["2024-09-29 09:56:53.681898+03", 15], ["2024-09-29 10:11:53.681898+03", 15],
 ["2024-09-29 10:26:53.681898+03", 15], ["2024-09-29 10:41:53.681898+03", 15]]
```
