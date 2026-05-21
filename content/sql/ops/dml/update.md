---
weight: 2
title: UPDATE
type: docs
bookToc: true
---

# UPDATE

```SQL
[WITH cte_name ...]
UPDATE [user.]table_name SET column[.path] = expr | DEFAULT [, ... ] 
[WHERE expr]
[RETURNING expr [INTO variable]]
```

Update rows in the table.

The Update operation is distributed and will transactionally update table partitions on one or more backends.
Update can be part of a multi-statement transaction.

If the user is not defined, the table name will be searched for the current user or agent.

The **`RETURNING`** clause allows the values to be returned in case of successful completion. The values can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

---

```SQL
CREATE TABLE example (
  id   int primary key using hash,
  data json
);
INSERT INTO example VALUES (1, {"list": []});

UPDATE example SET
  data.list = data.list::push_back(1,2,3)
WHERE
  id = 1
RETURNING *;

id  data
─────────────────────────
1   {"list": [1, 2, 3]}
```

```SQL
-- with CTE
WITH updated_items AS (
  UPDATE example SET data = data::append(4) WHERE id = 1 RETURNING *
) SELECT count(*) FROM updated_items;
```
