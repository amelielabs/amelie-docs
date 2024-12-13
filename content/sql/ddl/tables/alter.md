---
weight: 3
title: "ALTER TABLE"
bookToc: false
---

## ALTER TABLE Statement

```SQL
ALTER TABLE [IF EXISTS] [schema.]name RENAME TO [schema.]name
ALTER TABLE [IF EXISTS] [schema.]name SET SERIAL TO value
ALTER TABLE [IF EXISTS] [schema.]name COLUMN ADD name type [constraints]
ALTER TABLE [IF EXISTS] [schema.]name COLUMN DROP name
ALTER TABLE [IF EXISTS] [schema.]name COLUMN RENAME name TO name
```

Change the definition of a table if it exists.

Currently, the **`ALTER TABLE`** operation cannot be part of multi-statement transactions.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and **`ALTER TABLE ADD/DROP COLUMN`** are blocking but
completely parallel. Each worker node will create an index for its partitions.

**`ALTER TABLE ADD/DROP COLUMN`** is a memory-expensive operation that requires at least double
the memory size of the original table to complete while the previous table is kept. To avoid this
operation repeating during WAL replay, it is recommended to run the [CHECKPOINT](/docs/storage/checkpoint) operation right
after its completion.

Is recommended to organize tables by separating and creating volatile columns
using JSON (to store objects or arrays).

---

```SQL
create table example (device int primary key);
alter table example add column metrics json;
```
