---
weight: 13
title: "Common Table Expressions (CTE)"
bookToc: true
---

## Common Table Expressions

```SQL
WITH cte_name1 [(args)] AS ( statement ) [, cte_name2 ...]
```

CTE provides a way to define transactions where statements can use previous statements results.

CTE statements and statements without CTE can be used together. Multiple statements are separated
using the **;** symbol or defined using CTE.

Amelie generates an optimized parallel plan for executing multi-statement transactions and CTE.
It combines multiple requests together to reduce wait times and speed up the execution of
non-dependable CTE statements.

All DML statements have a **`RETURNING`** clause, which allows the assignment of CTE value
after its execution.

### RETURNING Clause

```SQL
RETURNING expression [AS alias][, ...]
```

All DML statements support a **`RETURNING`** clause, allowing the updated or
inserted data to be returned.

---

```SQL
-- with CTE
WITH deleted_items as (
    DELETE FROM collection RETURNING *
) SELECT count(*) FROM deleted_items;
```
