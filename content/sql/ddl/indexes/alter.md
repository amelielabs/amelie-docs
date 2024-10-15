---
weight: 3
title: "ALTER INDEX"
bookToc: false
---


## ALTER INDEX Statement

```SQL
ALTER INDEX [IF EXISTS] name ON [schema.]table_name RENAME TO name
```

Rename a table index.

If the schema is not defined, the table will be searched in the **`public`** schema.
The **`ALTER INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
create table metrics (id int primary key, ts timestamp) with (type = 'hash')
create index ts_idx on metrics (ts) with (type = 'tree')
alter index ts_idx on metrics rename to ts_renamed
```
