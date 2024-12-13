---
weight: 2
title: "DROP SCHEMA"
bookToc: false
---

## DROP SCHEMA Statement

```SQL
DROP SCHEMA [IF EXISTS] name [CASCADE]
```

Drop schema object if it exists.

The operation will fail if the schema still has associated objects unless
the **`CASCADE`** clause is used, which will recursively remove all objects in the schema.

System schemas **`system`** and **`public`** cannot be dropped.

---

```SQL
create schema example;
drop schema example;
```
