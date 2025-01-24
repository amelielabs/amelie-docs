---
weight: 1
title: "SELECT"
bookToc: false
---

## SELECT Statement

```SQL
[WITH cte_name ...]
SELECT [DISTINCT [ON (expr, ...)]] expr [AS alias] [, ...]
[[FROM [schema.]relation | cte | (SELECT ...) [, ...]
 [JOIN [schema.]relation | cte | (SELECT ...) ON (expr) [, ...] | USING (column)]
 [USE INDEX (name)]]
[WHERE expr]
[GROUP BY column_order | alias | expr[, ...] [HAVING expr]]
[ORDER BY column_order | alias | expr [ASC | DESC] [, ...]]
[LIMIT expr] [OFFSET expr]
[FORMAT type]
```

Retrieve rows from a table, CTE result, or subquery.

If the object schema is not defined, the object will be searched in the **`public`** schema.

Select operation is distributed and transactional and will be executed on one or more nodes if tables are
involved. Amelie is designed to split the work between partitions and compute nodes (**`PUSHDOWN`**).

Operations such as **`GROUP BY`**, **`ORDER BY`** and **`JOIN`** will be executed individually per
compute node in parallel. After the successful execution, the results of each computation are merged together,
processed, and returned.

Currently, only **`INNER JOIN`** is supported and will be extended in future releases. Joining distributed
tables directly has some limitations.

Select can be part of a multi-statement transaction and executed inside expressions (as subquery).

Amelie generates an optimized parallel plan for executing multi-statement transactions and CTE. It combines node
requests (pipeline) to reduce wait times and speed up the execution of non-dependable CTE statements.

Amelie is designed for short ACID transactions and fast real-time analytics. It is not intended for long, complex,
multi-statement transactions or queries that generate large amounts of data. There are configurable limits for
transaction size.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

### Index and Keys matching

By default, Amelie will try to use the most suitable index by matching keys by analyzing the **`WHERE`** expression.
It tries to identify whether the operation requires a **`range scan`** (start, stop conditions) or **`point lookup`** (by key).
This logic applies to the **`UPDATE`** and **`DELETE`** operations as well.

It is possible to force a query to use a specific index by using the **`USE INDEX`** clause for each table target. Primary index
keys are used for partitioning, where the primary or secondary index can be used by compute nodes for data scan
inside partitions.

### Distributed JOIN and Shared Tables

By default, all tables are **`DISTRIBUTED`**, meaning each distributed table will have partitions created on each node
for parallel access or modification. Currently, distributed tables cannot be used directly in a **`JOIN`** with other
distributed tables. However, they can be used in a multi-statement transaction or CTE.

There is also a particular type of table called **`SHARED`**. Those tables have only one partition and are available for
direct read access from any node. They can be used to implement efficient parallel **`JOIN`** operations with other
distributed tables. Frequent updating of a shared table is inefficient since it requires coordination and exclusive access.

### Subqueries

Currently, subqueries can be made to shared tables, and CTE results. Subqueries to other distributed tables
are not supported directly. Instead, CTE must be used. It will guarantee that a query to the distributed table is
executed only once and not nested.

---

```SQL
-- get the number of hits for the last hour for each device
create table example (
  time      timestamp,
  device_id int,
  primary key(time, device_id)
);

insert into example values ('2024-12-12 13:53:52.712025', 1);
insert into example values ('2024-12-12 14:20:52.712025', 1);
insert into example values ('2024-12-12 14:25:52.712025', 2);
insert into example values ('2024-12-12 14:27:52.712025', 1);

-- do parallel GROUP BY and ORDER BY on each compute node
select device_id, count(*) as hits
from example
where time >= timestamp '2024-12-12 14:30:00' - interval '1 hour'
group by 1
order by 1
format 'json-obj';
[{"device_id": 1, "hits": 3}, {"device_id": 2, "hits": 1}]
```

```SQL
-- using generated stored and resolved columns to
-- group inserts by 1 hour per device_id and aggregate hits
create table example (
  time      timestamp as ( time::date_bin(interval '1 hour') ) stored,
  device_id int,
  hits      int default 1 as ( hits + 1 ) resolved,
  primary key(time, device_id)
);

insert into example(time, device_id) values ('2024-12-12 13:53:52.712025', 1);
insert into example(time, device_id) values ('2024-12-12 14:20:52.712025', 1);
insert into example(time, device_id) values ('2024-12-12 14:25:52.712025', 2);
insert into example(time, device_id) values ('2024-12-12 14:27:52.712025', 1);

-- GROUP BY is not needed, since rows are already aggregated
select time, device_id, hits
from example
order by 1
format 'json-obj-pretty';
[{
  "time": "2024-12-12 13:00:00+02",
  "device_id": 1,
  "hits": 1
}, {
  "time": "2024-12-12 14:00:00+02",
  "device_id": 2,
  "hits": 1
}, {
  "time": "2024-12-12 14:00:00+02",
  "device_id": 1,
  "hits": 2
}]
```

```SQL
-- similarity search using vector
create table example (id serial primary key, embedding vector);
insert into example (embedding) values ([3,2,0,1,4]);
insert into example (embedding) values ([2,2,0,1,3]);
insert into example (embedding) values ([1,3,0,1,4]);
select * from example;
[[0, [3, 2, 0, 1, 4]], [1, [2, 2, 0, 1, 3]], [2, [1, 3, 0, 1, 4]]]

-- order rows by similarity
select id, embedding::cos_distance(vector [1,3,1,2,0])
from example
order by 2 desc;
[[1, 0.481455], [2, 0.403715], [1, 0.391419]]

-- find the most alike row
select id from example
order by embedding::cos_distance(vector [1,3,1,2,0]) desc
limit 1;
[0]
```

```SQL
-- JSON expressions
select {"at": current_timestamp, "id": system.config().uuid};
[{
  "at": "2024-09-26 16:14:00.722393+03",
  "id": "a74fbf39-cc9d-314e-a33e-3aa47559ffe5"
}]

select {"total": select count(*) from example};
[{
  "total": 3
}]
```

```SQL
-- distributed JOIN using shared dictionary table
create table collection(id int primary key);
create shared table dict(id int primary key) with (type = 'hash');

insert into dict values (1), (3);
insert into collection values (1), (2), (3);

select c.* from collection c join dict on (dict.id = c.id);
[[1], [3]]
```

```SQL
-- distributed JOIN using CTE
create table t1 (id int primary key);
create table t2 (id int primary key);

insert into t1 values (1), (3);
insert into t2 values (1), (2), (3);

-- t1_result will be passed down for parallel JOIN with t2
with t1_result (id) as (
    select * from t1
) select t2.* from t2 join t1_result on (t2.id = t1_result.id);
[[1], [3]]
```
