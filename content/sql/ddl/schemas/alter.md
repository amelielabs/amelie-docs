---
weight: 3
title: "ALTER SCHEMA"
bookToc: false
---

## ALTER SCHEMA Statement

```SQL
ALTER SCHEMA [IF EXISTS] name RENAME TO name
```

Rename the schema object if it exists.

The operation will recursively rename schemas of the associated objects.

System schemas **`system`** and **`public`** cannot be altered.

---

```SQL
create schema test
alter schema test rename to example
drop schema example
```
