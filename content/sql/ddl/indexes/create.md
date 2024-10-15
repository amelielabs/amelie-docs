---
weight: 1
title: "CREATE INDEX"
bookToc: false
---

## CREATE INDEX Statement

```SQL
CREATE [UNIQUE] INDEX [IF NOT EXISTS] name ON [schema.]table_name (key[, ...])
[WITH (option[, ...])]

key:
	column name | path type

type:
	int
	real
	bool
	text
	object
	array
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

Amelie supports primary and secondary indexes on **`OBJECT`** column fields. In such cases, the index key
must be provided with the search path and the key type.

Operations such as **`CREATE INDEX`** and [ALTER TABLE ADD/DROP COLUMN](/docs/sql/ddl/tables/alter) are blocking but completely parallel.
Each node will create an index for its partitions. To avoid this operation repeating during WAL replay, it is recommended to
run the [CHECKPOINT](/docs/storage/checkpoint) operation right after its completion.

Currently, the **`CREATE INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
create table metrics (id int primary key, ts timestamp) with (type = 'hash')
create index ts_idx on metrics (ts) with (type = 'tree')

select indexes from system.tables() where name = 'metrics'
[[{
  "name": "primary",
  "type": 1,
  "unique": true,
  "primary": true,
  "keys": [{
    "ref": 0,
    "type": "int",
    "path": ""
  }]
}, {
  "name": "ts_idx",
  "type": 2,
  "unique": false,
  "primary": false,
  "keys": [{
    "ref": 1,
    "type": "timestamp",
    "path": ""
  }, {
    "ref": 0,
    "type": "int",
    "path": ""
  }]
}]]
```

```SQL
create shared table test (id int primary key serial, obj object)
create index obj_idx on test (obj.id int)

insert into test (obj) values ({"id": 56}), ({"id": 48})

select * from test
[[0, {
  "id": 56
}], [1, {
  "id": 48
}]]

select * from test use index (obj_idx)
[[1, {
  "id": 48
}], [0, {
  "id": 56
}]]
```
