---
weight: 1
title: "CREATE TABLE"
bookToc: false
---

## CREATE TABLE Statement

```SQL
CREATE [UNLOGGED] TABLE [IF NOT EXISTS] [schema.]name
(column [, ...] [, primary key (keys)])
[PARTITIONS count]
[WITH (options)]

column:
	name type [constraints]

type:
	bool
	tinyint
	smallint
	int
	bigint
	serial
	float
	double
	text
	json
	timestamp
	interval
	date	
	vector
	uuid

constraints:
	NOT NULL
	DEFAULT const
	PRIMARY KEY
	[ALWAYS GENERATED] AS [(expr)] <IDENTITY | STORED | RESOLVED>

primary key:
	PRIMARY KEY [(column_name[, ...])] 

options:
	name = expr [,...]
```

Create a new table if it does not exist.

If the schema name is not defined, it will be set to **`public`** by default. One or more columns must be
defined as a **`PRIMARY KEY`**. Currently, only **`INT`**, **`STRING`**, **`TIMESTAMP`** and **`UUID`** columns can
be used as part of a key.

The table **`primary`** index will be automatically created using a defined index type and the primary key.
The primary index is always created as **`UNIQUE`**. Supported index types are **`hash`** and **`tree`**. The index type can
be selected using the **`WITH`** clause. If the index type is not defined, it will default to **`tree`**.

All tables are automatically partitioned (hash partitioning), and partitions are created on one or
more backends. Amelie uses consistent hashing to assign each partition interval to a backend worker.

**`PRIMARY KEY`** columns are used as the partition key.

Organizing tables by separating and creating volatile columns as JSON values (objects and arrays) is recommended.
It is possible to index JSON documents by creating table keys as generated columns which
point to other column JSON data.

Currently, the **`CREATE TABLE`** operation cannot be part of multi-statement transactions.

### Partitioned Tables

All tables are partitioned and distributed across CPU cores. Partitions will be created on each backend worker for parallel access or modification.
The number of partitions can be specified using the **`PARTITIONS`** clause. If the number of partitions is not
defined, it will be set to the number of backends. The table cannot have more partitions than the current number of active backends.

Partitioned tables can be directly joined with other partitioned tables and used in subqueries.
Amelie coordinates access to partitions created on other backends for those cases to avoid concurrent
writes simultaneously.

Additionally, expressions or CTE can be used to JOIN data. Amelie treats [CTE](/docs/sql/transactions/cte) as separate
statements to combine and execute non-dependable statements in one operation on backend workers. The query planner
tries to rewrite queries using CTE whenever it can.

### Unlogged Tables

Any table can be created using the **`UNLOGGED`** clause.

The unlogged tables DML will be excluded from WAL (and replication streaming), and the table's data will be saved
during the database [CHECKPOINT](/docs/reliability/checkpoint) and recovered upon restart from the last checkpoint.

Unlogged tables can provide an additional performance boost for highly volatile tables.

### Generated Columns

Amelie supports several types of generated columns:

* **`ALWAYS GENERATED AS IDENTITY`**
  
  Identity columns allow you to automatically assign a unique number to a column. If a table has more than
  one identity column, they will share the same value. Only columns with **`INT`** and **`BIGINT`** types can be
  used as identity columns.

  Using **`SERIAL`** as a column type will make the column as an identity column using **`BIGINT`** type.

* **`ALWAYS GENERATED AS (expr) STORED`**

  The content of all stored generated columns will be automatically updated during insert
  using the expression's result. Amelie allows the user to reuse (access) the provided value for
  the generated column, which can be used to dynamically change the partition key.

* **`ALWAYS GENERATED AS (expr) RESOLVED`**

  **`RESOLVED`** columns are a unique feature of Amelie that allows you to specify expressions that
  will be executed automatically when a primary key constraint is violated to resolve conflicts.
  If the table has resolved columns, **`INSERT`** operations (without explicit **`ON CONFLICT CLAUSE`**)
  will be rewritten as upsert **`INSERT ON CONFLICT DO UPDATE`** using the resolved expressions as
  the update expressions.

---

```SQL
create table metrics (
  device_id int primary key,
  data json
) with (type = 'hash');

insert into metrics values (42, [1,2,3]);

select * from metrics;
[[42, [1, 2, 3]]]

select {"id": device_id, "metrics": data} from metrics;
[{
  "id": 42,
  "metrics": [1, 2, 3]
}]

select * format 'json-obj-pretty' from metrics;
[{
  "device_id": 42,
  "data": [1, 2, 3]
}]
```

```SQL
-- using generated columns to indexate JSON data
create table example (
  id   int primary key as (data.id::int) stored,
  data json
);

insert into example (data) values ({"id": 1}), ({"id": 2}), ({"id": 3});

select id from example;
[1, 2, 3]
```

```SQL
--
-- using generated stored and resolved columns to
-- group inserts by last 5 seconds per device_id and aggregate hits
--
create table example (
  time      timestamp as ( current_timestamp::date_bin(interval '5 sec') ) stored,
  device_id int,
  hits      int default 1 as ( hits + 1 ) resolved,
  primary key(time, device_id)
);

insert into example (device_id) values (1);
insert into example (device_id) values (1);
insert into example (device_id) values (1);
insert into example (device_id) values (1);

select * from example;
[["2024-12-11 17:03:30+02", 1, 4]]
```
