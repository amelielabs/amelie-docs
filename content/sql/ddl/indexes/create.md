---
weight: 1
title: "CREATE INDEX"
bookToc: false
---

## CREATE INDEX Statement

```SQL
CREATE [UNIQUE] INDEX [IF NOT EXISTS] name ON [schema.]table_name (column[, ...])
[WITH (option[, ...])]

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

option:
	name = expr
```

Create a secondary index.

All primary indexes are always **`UNIQUE`**. Secondary unique indexes for distributed tables are not supported.
The **`UNIQUE`** indexes can be created only with shared tables.

Currently, supported index types are **`hash`** and **`tree`**. The **`WITH`** clause allows you to select the index type.
If the index type is not defined, it will default to the **`tree`**.

Operations such as **`CREATE INDEX`** and [ALTER TABLE ADD/DROP COLUMN](/docs/sql/ddl/tables/alter) are blocking but completely parallel.
Each node will create an index for its partitions. To avoid this operation repeating during WAL replay, it is recommended to
run the [CHECKPOINT](/docs/storage/checkpoint) operation right after its completion.

It is possible to index JSON documents by creating table keys as generated columns which
point to other column JSON data.

Currently, the **`CREATE INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
create table metrics (id int primary key, ts timestamp) with (type = 'hash')
create index ts_idx on metrics (ts) with (type = 'tree')
```
