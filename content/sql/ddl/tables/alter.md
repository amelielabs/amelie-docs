---
weight: 4
title: "ALTER TABLE"
bookToc: true
---

# ALTER TABLE

```SQL
ALTER TABLE [IF EXISTS] name RENAME TO name
ALTER TABLE [IF EXISTS] name SET IDENTITY TO value
ALTER TABLE [IF EXISTS] name ADD COLUMN [IF NOT EXISTS] name type [constraint]
ALTER TABLE [IF EXISTS] name DROP COLUMN [IF EXISTS] name
ALTER TABLE [IF EXISTS] name RENAME COLUMN [IF EXISTS] name TO name
ALTER TABLE [IF EXISTS] name SET COLUMN [IF EXISTS] name DEFAULT const
ALTER TABLE [IF EXISTS] name UNSET COLUMN [IF EXISTS] name DEFAULT
ALTER TABLE [IF EXISTS] name ADD STORAGE [IF NOT EXISTS] name [(options])
ALTER TABLE [IF EXISTS] name DROP STORAGE [IF EXISTS] name
ALTER TABLE [IF EXISTS] name PAUSE STORAGE [IF EXISTS] name
ALTER TABLE [IF EXISTS] name RESUME STORAGE [IF EXISTS] name
```

Change the definition of a table if it exists.

Currently, the **`ALTER TABLE`** operation cannot be part of multi-statement transactions.

Operations such as [CREATE INDEX](/docs/sql/ddl/indexes/create) and [ALTER TABLE ADD COLUMN](/docs/sql/ddl/tables/alter) are
non-blocking. Each backend worker will be involved in creating an index for its partitions incrementally and concurrently.

The **ADD COLUMN** and **DROP COLUMN** are instant operations. It changes only the catalog metadata. Actual
column-dropped column data will remain in the rows and eventually be removed.

Is recommended to organize tables by separating and creating volatile columns
using JSON (to store objects or arrays).

---
