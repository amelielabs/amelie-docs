---
weight: 1
title: INSERT / UPSERT
type: docs
bookToc: true
---

# INSERT


```SQL
[WITH cte_name ...]
INSERT INTO [user.]name [(column_list)]
VALUES (value, ..), ... | SELECT ...
[ON CONFLICT DO NOTHING | ERROR | RESOLVE | UPDATE ... [WHERE]]
[RETURNING expr [INTO variable]]
```

Insert one or more rows into the table.

The Insert operation is distributed and will transactionally update table partitions on one or more backends.
Insert can be part of a multi-statement transaction.

If the user is not defined, the table name will be searched for the current user or agent.

If the column list is not defined, all values must correspond to the table column types. If the column list is
defined, only the list-defined columns will be set to the corresponding values. Non-defined column values will be
set to **`NULL`**, **`SERIAL`** value or **`DEFAULT`** value will be used (if defined).
If more than one identity columns columns are used, they will share the same value.

If the row already exists (according to the primary key), the table primary index unique constraint violation error
will be emitted. The **`ON CONFLICT`** clause allows to change this behavior:

* **`ON CONFLICT DO NOTHING`**

  If the key already exists, ignore the operation.

* **`ON CONFLICT DO ERROR`**

  If the key already exists, throw an error (default INSERT behaviour).

* **`ON CONFLICT DO RESOLVE`**

  If the table has resolved columns, the **`INSERT`** operation will be automatically rewritten as
  update **`INSERT ON CONFLICT DO UPDATE`** using the resolved expressions as
  the update expressions.
  
  If the table has no resolved columns, this operation will be equal
  to **`ON CONFLICT DO ERROR`**.

* **`ON CONFLICT DO UPDATE`**

  If the key already exists, apply the [UPDATE](/docs/sql/ops/dml/update) statement on the existing key.
  The **`excluded.<column>`** prefix can be used to access the inserted row columns.
  Additionally, the **`WHERE`** clause can be used to filter rows.

The **`RETURNING`** clause allows the values to be returned in case of successful completion. The values can
be used as a result in the corresponding [CTE](/docs/sql/transactions/cte) or as a standalone result.

## Data Ingestion and Streaming

An alternative way to insert data directly into a table without using **`SQL`** is to use the
[JSON-RPC API](/docs/api/http).

---

```SQL
CREATE TABLE example (
  id      int primary key using hash,
  matches int
);
INSERT INTO example VALUES (1, 0);
INSERT INTO example VALUES (1, 0)
    ON CONFLICT DO UPDATE SET matches = matches + 1;
INSERT INTO example VALUES (1, 0)
    ON CONFLICT DO UPDATE SET matches = matches + 1;
SELECT * FROM example;

id  matches
─────────────
1   2
```

```SQL
CREATE TABLE example (
  device_id int primary key using hash,
  hits      int default 1 as ( hits + 1 ) resolved
);
INSERT INTO example (device_id) VALUES (1);
INSERT INTO example (device_id) VALUES (1) ON CONFLICT DO RESOLVE;
INSERT INTO example (device_id) VALUES (1) ON CONFLICT DO RESOLVE;

-- ON CONFLICT DO RESOLVE can be ommited, if the table
-- has resolved columns
INSERT INTO example (device_id) VALUES (1);
SELECT * FROM example;

device_id  hits
─────────────────
1          4
```

```SQL
-- with CTE
WITH inserted_items AS (
    INSERT INTO example VALUES (1), (2), (3) RETURNING *
) SELECT count(*) FROM inserted_items;
```
