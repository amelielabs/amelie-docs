---
weight: 1
title: "SELECT"
bookToc: false
---

## SELECT Statement

```SQL
[WITH cte_name ...]
SELECT [DISTINCT [ON (expr, ...)]] expr [AS alias] [, ...]
[[FROM [schema.]relation | cte | (expr | SELECT ...) [, ...]
 [JOIN [schema.]relation | cte | (expr | SELECT ...) ON (expr) [, ...] | USING (column)]
 [USE INDEX (name)]]
[WHERE expr]
[GROUP BY column_order | alias | expr[, ...] [HAVING expr]]
[ORDER BY column_order | alias | expr [ASC | DESC] [, ...]]
[LIMIT expr] [OFFSET expr]
[FORMAT type]
```

Retrieve rows from a table, CTE result, expression, or subquery.

If the object schema is not defined, the object will be searched in the **`public`** schema.

Select operation is distributed and transactional and will be executed on one or more backends if tables are
involved. Amelie is designed to split the work between partitions and backend workers (**`PUSHDOWN`**).

Operations such as **`GROUP BY`**, **`ORDER BY`** and **`JOIN`** will be executed individually per
backend in parallel. After the successful execution, the results of each computation are merged together,
processed, and returned.

Currently, only **`INNER JOIN`** is supported and will be extended in future releases. Joining partitioned
tables directly has some limitations.

Select can be part of a multi-statement transaction and executed inside expressions (as subquery).

Amelie generates an optimized parallel plan for executing multi-statement transactions and CTE. It combines
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
keys are used for partitioning, where the primary or secondary index can be used by backends for data scan
inside partitions.

### HEAP-only scan

Using the **`USE HEAP`** clause, it is possible to force a query read directly from a memory allocator
context to avoid using indexes.

### Parallel JOIN and Subqueries

All tables are partitioned and distributed across CPU cores. Partitions will be created on each backend worker for parallel access or modification.

Partitioned tables can be directly joined with other partitioned tables and used in subqueries.
Amelie coordinates access to partitions created on other backends for those cases to avoid concurrent
writes simultaneously.

Additionally, expressions or CTE can be used to JOIN data. Amelie treats [CTE](/docs/sql/transactions/cte) as separate
statements to combine and execute non-dependable statements in one operation on backend workers. The query planner
tries to rewrite queries using CTE whenever it can.

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

-- do parallel GROUP BY and ORDER BY on each backend
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
-- UPDATE using subquery
--
-- Pushdown UPDATE to each related table partition (to each backend worker per cpu
-- core for parallel update) with coordinated point lookup access to
-- other partitioned table.
--
explain update test set data = data + 1 where exists (select true from ref where id = test.id)
[{
  "bytecode": {
    "frontend": {
      "00": "send_all            0      0      -     # public.test",
      "01": "recv                0      0      0     ",
      "02": "null                0      0      0     ",
      "03": "cte_set             0      0      0     ",
      "04": "ret                 0      0      0     "
    },
    "backend": {
      "00": "table_open_part     0      0      23    # public.test (primary)",
      "01": "set                 0      1      0     ",
      "02": "table_readi32       1      0      0     ",
      "03": "push                1      0      0     ",
      "04": "table_openl         1      20     12    # public.ref (primary)",
      "05": "table_readi32       1      1      0     ",
      "06": "table_readi32       2      0      0     ",
      "07": "equii               3      1      2     ",
      "08": "jntr                12     3      0     ",
      "09": "bool                1      1      0     ",
      "10": "push                1      0      0     ",
      "11": "set_add             0      0      0     ",
      "12": "table_close         1      0      0     ",
      "13": "exists              1      0      0     ",
      "14": "jntr                22     1      0     ",
      "15": "int                 0      -      0     # 1",
      "16": "push                0      0      0     ",
      "17": "table_readi32       0      0      1     ",
      "18": "int                 1      -      0     # 1",
      "19": "addii               2      0      1     ",
      "20": "push                2      0      0     ",
      "21": "update              0      1      0     ",
      "22": "table_next          0      1      0     ",
      "23": "table_close         0      0      0     ",
      "24": "ret                 0      0      0     "
    }
  },
  "access": [["public.test", "rw"], ["public.ref", "ro_exclusive"]]
}]
```
