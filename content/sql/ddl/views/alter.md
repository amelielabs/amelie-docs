---
weight: 3
title: "ALTER VIEW"
bookToc: false
---

## ALTER VIEW Statement

```SQL
ALTER VIEW [IF EXISTS] [schema.]name RENAME TO [schema.]name
```

Rename a view object.

If the schema is not defined, the view will be searched in the **`public`** schema.
The **`ALTER VIEW`** operation cannot be part of multi-statement transactions.

---

```SQL
create view test as select [1,2,3]
alter view public.test rename to public.test_renamed
```
