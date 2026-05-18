---
weight: 1
title: "CREATE INDEX"
bookToc: true
---

# CREATE INDEX Statement

```SQL
CREATE [UNIQUE] INDEX [IF NOT EXISTS] name ON table_name (keys)
[USING type]
```

```text
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

option:
	name = expr
```

Create a secondary index.

All primary indexes are always **`UNIQUE`**. Secondary unique indexes are supported if the table has one partition.

Currently, supported index types are **`hash`** and **`tree`**. The **`USING`** clause allows you to select the index type.
If the index type is not defined, it will default to the **`tree`**.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and [ALTER TABLE ADD COLUMN](/docs/sql/ddl/tables/alter) are
non-blocking. Each backend worker will be involved in creating an index for its partitions incrementally and concurrently.

It is possible to index JSON documents by creating table keys as generated columns which
point to other column JSON data.

Currently, the **`CREATE INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
CREATE TABLE metrics (id int primary key using hash, ts timestamp);
CREATE INDEX metrics_ts_idx ON metrics (ts) USING tree;
```
