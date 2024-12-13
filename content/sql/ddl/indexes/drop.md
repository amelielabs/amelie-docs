---
weight: 2
title: "DROP INDEX"
bookToc: false
---

## DROP INDEX Statement

```SQL
DROP INDEX [IF EXISTS] name ON [schema.]table_name
```

Drop table index.

If the schema is not defined, the table will be searched in the **`public`** schema.
The **`DROP INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
create table metrics (id int primary key, ts timestamp) with (type = 'hash');
create index ts_idx on metrics (ts) with (type = 'tree');
drop index ts_idx on metrics;
```
