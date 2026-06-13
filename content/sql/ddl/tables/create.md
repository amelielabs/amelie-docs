---
weight: 2
title: "CREATE TABLE"
bookToc: true
---

# CREATE TABLE

```SQL
CREATE TABLE [IF NOT EXISTS] name
(column [, ...] [, PRIMARY KEY (keys)])
[PARTITIONS count]
[WITH (options)]
[DESCRIPTION text]
```

```text
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
	DEFAULT value
	PRIMARY KEY [USING index_type]
	[[ALWAYS GENERATED] AS IDENTITY]

primary key:
	PRIMARY KEY [(column_name[, ...])] 

options:
	name = expr [,...]
```

Create a new table if it does not exists.

The current user or agent becomes the owner of the table.

One or more columns must be defined as a **`PRIMARY KEY`**. Currently, only **`INT`**, **`STRING`**,
**`TIMESTAMP`** and **`UUID`** columns can be used as part of a key.

The table **`primary`** index will be automatically created using a defined index type and the primary key.
The primary index is always created as **`UNIQUE`**.

The index type can be selected with the **`USING`** clause.
Supported index types are **`hash`** and **`tree`**. If the index type is not defined, it will
default to **`tree`**.

All tables are automatically partitioned (hash partitioning), and partitions are created on one or
more backends. Amelie uses consistent hashing to assign each partition interval to a partition.

**`PRIMARY KEY`** columns are used as the partition key.

Organizing tables by separating and creating volatile columns as JSON values (objects and arrays) is recommended.

Currently, the **`CREATE TABLE`** operation cannot be part of multi-statement transactions.

## Partitioning

All tables are partitioned (having at least 1 partition). Partitions will be created
on each backend worker for parallel access or modification.

The number of partitions can be specified using the **`PARTITIONS`** clause. If the number of partitions is not
defined, it will be set to the number of backends. The table can have more partitions than the current number of active backends.

Tables can be directly joined with other tables and used in subqueries.
Amelie coordinates access to partitions created on other backends for those cases to avoid concurrent
writes simultaneously.

Additionally, expressions or CTE can be used to JOIN data. Amelie treats [CTE](/docs/sql/transactions/cte) as separate
statements to combine and execute non-dependable statements in one operation on backend workers. The query planner
tries to rewrite queries using CTE whenever it can.

## Generated Columns

Amelie supports following types of generated columns:

* **`ALWAYS GENERATED AS IDENTITY`**
  
  Identity columns allow you to automatically assign a unique number to a column. If a table has more than
  one identity column, they will share the same value. Only columns with **`INT`** and **`BIGINT`** types can be
  used as identity columns.

  Using **`SERIAL`** as a column type will make the column as an identity column using **`BIGINT`** type.

---

```SQL
CREATE TABLE metrics (
  device_id int primary key using hash,
  state     json,
  updates   int default 1
);

INSERT INTO metrics (device_id, state)
VALUES
  (1, {"temp": 42}),
  (2, {"temp": 38}),
  (1, {"temp": 39})
ON CONFLICT DO UPDATE SET
  state   = excluded.state,
  updates = updates + 1;

SELECT * FROM metrics;

device_id  state         updates
──────────────────────────────────
1          {"temp": 39}  2
2          {"temp": 38}  1
```
