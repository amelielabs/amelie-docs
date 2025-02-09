---
weight: 13
title: "Common Table Expression (CTE)"
bookToc: false
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
RETURNING expression [AS alias][, ...] [FORMAT 'type']
```

All DML statements support a **`RETURNING`** clause, allowing the updated or
inserted data to be returned.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
-- with CTE
with deleted_items as (
    delete from collection returning *
) select count(*) from deleted_items;
[3]
```
