---
weight: 1
title: "CREATE TABLE"
bookToc: false
---

## CREATE TABLE Statement

```SQL
CREATE [SHARED | DISTRIBUTED] TABLE [IF NOT EXISTS] [schema.]name
(column [, ...] [, primary key (keys)])
[WITH (options)]

column:
	name type [constraints]

type:
	bool
	tinyint
	smallint
	int
	bigint
	float
	double
	text
	json
	timestamp
	interval
	vector

constraints:
	NOT NULL
	DEFAULT const
	SERIAL
	PRIMARY KEY
	[ALWAYS GENERATED] AS (expr) <STORED | RESOLVED>

primary key:
	PRIMARY KEY [(column_name[, ...])] 

options:
	name = expr [,...]
```

Create a new table if it does not exist.

If the schema name is not defined, it will be set to **`public`** by default. One or more columns must be
defined as a **`PRIMARY KEY`**. Currently, only **`INT`**, **`STRING`**, and **`TIMESTAMP`** columns can be used as
part of a key.

The table **`primary`** index will be automatically created using a defined index type and the primary key.
The primary index is always created as **`UNIQUE`**. Supported index types are **`hash`** and **`tree`**. The index type can
be selected using the **`WITH`** clause. If the index type is not defined, it will default to **`tree`**.

All tables are automatically partitioned (hash partitioning), and partitions are created on one or
more nodes. Amelie uses consistent hashing to assign each partition interval to a node. **`PRIMARY KEY`**
columns are used as the partition key.

Organizing tables by separating and creating volatile columns as JSON values (objects and arrays) is recommended.
It is possible to index JSON documents by creating table keys as generated columns which
point to other column JSON data.

Currently, the **`CREATE TABLE`** operation cannot be part of multi-statement transactions.

There are two types of tables: **`DISTRIBUTED`** and **`SHARED`**.

### Distributed Tables

By default, all tables are **`DISTRIBUTED`**, meaning each distributed table will have partitions
created on each node for parallel access or modification. Currently, distributed tables cannot
be used directly in a JOIN with other distributed tables. However, they can be used in a multi-statement
transaction or [CTE](/docs/sql/transactions/cte).

### Shared Tables

There is also a particular type of table called **`SHARED`**. Those tables have only one partition and are
available for direct read access from any node. Their primary purpose is to implement efficient **`parallel
JOIN`** operations with other distributed tables. Frequent updating of a shared table is
less efficient since it requires coordination and exclusive access.

### Generated Columns

Amelie supports two types of generated columns: **`STORED`** and **`RESOLVED`**.

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

insert into metrics values (42, [1,2,3])

select * from metrics
[[42, [1, 2, 3]]]

select * format 'json-obj-pretty' from metrics
[{
  "device_id": 42,
  "data": [1, 2, 3]
}]

select {"id": device_id, "metrics": data} from metrics
[{
  "id": 42,
  "metrics": [1, 2, 3]
}]
```

```SQL
--- using generated columns to indexate JSON data
create table test (
  id   int primary key as (data.id::int) stored,
  data json
)

insert into test (data) values ({"id": 1}), ({"id": 2}), ({"id": 3})

select id from test
[1, 2, 3]
```

```SQL
--
-- using generated stored and resolved columns to
-- group inserts by last 5 seconds per device_id and aggregate hits
--
create table test (
  time      timestamp as ( current_timestamp::date_bin(interval '5 sec') ) stored,
  device_id int,
  hits      int default 1 as ( hits + 1 ) resolved,
  primary key(time, device_id)
)

insert into test (device_id) values (1)
insert into test (device_id) values (1)
insert into test (device_id) values (1)
insert into test (device_id) values (1)

select * from test
[["2024-12-11 17:03:30+02", 1, 4]]
```
