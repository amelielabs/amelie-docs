---
weight: 2
title: "DROP TABLE"
bookToc: false
---

## DROP TABLE Statement

```SQL
DROP TABLE [IF EXISTS] [schema.]name
```

Drop table object if it exists.

If the schema is not defined, the table will be searched in the **`public`** schema.
The **`DROP TABLE`** operation cannot be part of multi-statement transactions.

---

```SQL
drop table public.example;
```
