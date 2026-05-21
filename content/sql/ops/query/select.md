---
weight: 1
title: "SELECT"
bookToc: true
---

# SELECT

```SQL
[WITH cte_name ...]
SELECT [DISTINCT [ON (expr, ...)]] expr [AS alias] [, ...]
[INTO variable]
[[FROM [user.]relation | cte | variable | (expr | SELECT ...) [, ...]
 [JOIN [user.]relation | cte | variable | (expr | SELECT ...) ON (expr) [, ...] | USING (column)]
 [USE INDEX (name)] |
 [FROM SHOW ...]]
[WHERE expr]
[GROUP BY column_order | alias | expr[, ...] [HAVING expr]]
[ORDER BY column_order | alias | expr [ASC | DESC] [, ...]]
[LIMIT expr] [OFFSET expr]
```

Retrieve rows from a table, CTE result, expression, variable or subquery.

If the user is not defined, the table name will be searched for the current user or agent.

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

## Index and Keys matching

By default, Amelie will try to use the most suitable index by matching keys by analyzing the **`WHERE`** expression.
It tries to identify whether the operation requires a **`range scan`** (start, stop conditions) or **`point lookup`** (by key).
This logic applies to the **`UPDATE`** and **`DELETE`** operations as well.

It is possible to force a query to use a specific index by using the **`USE INDEX`** clause for each table target. Primary index
keys are used for partitioning, where the primary or secondary index can be used by backends for data scan
inside partitions.

## Parallel JOIN and Subqueries

All tables are partitioned and distributed across CPU cores. Partitions will be created on each
backend worker for parallel access or modification.

Tables can be directly joined with other tables and used in subqueries.
Amelie coordinates access to partitions created on other backends for those cases to avoid concurrent
writes simultaneously.

Additionally, expressions or CTE can be used to JOIN data. Amelie treats [CTE](/docs/sql/transactions/cte) as separate
statements to combine and execute non-dependable statements in one operation on backend workers. The query planner
tries to rewrite queries using CTE whenever it can.

---

```SQL
-- get the number of hits for the last hour for each device
CREATE TABLE example (
  time      timestamp,
  device_id int,
  primary key(time, device_id)
);

INSERT INTO example VALUES ('2024-12-12 13:53:52.712025', 1);
INSERT INTO example VALUES ('2024-12-12 14:20:52.712025', 1);
INSERT INTO example VALUES ('2024-12-12 14:25:52.712025', 2);
INSERT INTO example VALUES ('2024-12-12 14:27:52.712025', 1);

-- do parallel GROUP BY and ORDER BY on each backend
SELECT device_id, count(*) as hits
  FROM example
 WHERE time >= timestamp '2024-12-12 14:30:00' - interval '1 hour'
 GROUP By 1
 ORDER BY 1;

device_id  hits
─────────────────
1          3
2          1
```

```SQL
-- using generated stored and resolved columns to
-- group inserts by 1 hour per device_id and aggregate hits
CREATE TABLE example (
  time      timestamp as ( time::date_bin(interval '1 hour') ) stored,
  device_id int,
  hits      int default 1 as ( hits + 1 ) resolved,
  primary key(time, device_id) using hash
);

INSERT INTO example(time, device_id) VALUES ('2024-12-12 13:53:52.712025', 1);
INSERT INTO example(time, device_id) VALUES ('2024-12-12 14:20:52.712025', 1);
INSERT INTO example(time, device_id) VALUES ('2024-12-12 14:25:52.712025', 2);
INSERT INTO example(time, device_id) VALUES ('2024-12-12 14:27:52.712025', 1);

-- GROUP BY is not needed, since rows are already aggregated
SELECT time, device_id, hits
  FROM example
 ORDER BY 1;

time                              device_id  hits
───────────────────────────────────────────────────
2024-12-12 13:00:00+02            1          1
2024-12-12 14:00:00+02            2          1
2024-12-12 14:00:00+02            1          2
```

```SQL
-- similarity vector search
CREATE TABLE example (id serial primary key, embedding vector);
INSERT INTO example (embedding) values ([3,2,0,1,4]);
INSERT INTO example (embedding) values ([2,2,0,1,3]);
INSERT INTO example (embedding) values ([1,3,0,1,4]);
SELECT * FROM example;

id  embedding
─────────────────────
0   [3, 2, 0, 1, 4]
1   [2, 2, 0, 1, 3]
2   [1, 3, 0, 1, 4]

-- order rows by similarity
SELECT
   id, embedding::cos_distance(vector [1,3,1,2,0])
FROM
   example
ORDER BY 2 desc;

id  cos_distance
──────────────────
0   0.481455
2   0.403715
1   0.391419
```

```SQL
-- JSON expressions
SELECT {"at": current_timestamp, "id": show().uuid} as json;

json
────
{
  "at": "2026-05-17 17:08:19.596411+03",
  "id": "b9b6fbf1-85de-9a0b-63e2-3233e03c6803"
}
```

```SQL
SELECT * FROM SHOW TABLES;

tables
──────
{
  "user": "amelie",
  "name": "metrics"
}
{
  "user": "amelie",
  "name": "example"
}
```
