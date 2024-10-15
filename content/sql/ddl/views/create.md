---
weight: 1
title: "CREATE VIEW"
bookToc: false
---

## CREATE VIEW Statement

```SQL
CREATE VIEW [IF NOT EXISTS] [schema.]name [(args)]
AS SELECT ...
```

Create a view object.

If the schema name is not defined, it will be set to **`public`** by default.
Currently, the **`CREATE VIEW`** operation cannot be part of multi-statement transactions.

---

```SQL
create view test as select [1,2,3]
select * from test
[1, 2, 3]
```
