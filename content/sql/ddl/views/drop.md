---
weight: 2
title: "DROP VIEW"
bookToc: false
---

## DROP VIEW Statement

```SQL
DROP VIEW [IF EXISTS] [schema.]name
```

Drop view object if it exists.

If the schema is not defined, the view will be searched in the **`public`** schema.
The **`DROP VIEW`** operation cannot be part of multi-statement transactions.

---

```SQL
create view test as select [1,2,3]
drop view public.test
```
