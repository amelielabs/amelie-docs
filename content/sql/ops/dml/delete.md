---
weight: 3
title: DELETE
type: docs
bookToc: true
---

# DELETE

```SQL
[WITH cte_name ...]
DELETE FROM [user.]table_name
[WHERE expr]
[RETURNING expr [INTO variable]]
```

Delete rows in the table.

The Delete operation is distributed and will transactionally update table partitions on one or more backends.
Delete can be part of a multi-statement transaction.

If the user is not defined, the table name will be searched for the current user or agent.

The **`RETURNING`** clause allows the values to be returned in case of successful completion. The values can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

---

```SQL
DELETE FROM example RETURNING *;

id  data
─────────────────────────
1   {"list": [1, 2, 3]}
```

```SQL
-- with CTE
WITH deleted_items as (
    DELETE FROM example RETURNING *
) SELECT count(*) FROM deleted_items;
```
