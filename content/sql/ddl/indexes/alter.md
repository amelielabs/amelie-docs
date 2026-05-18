---
weight: 3
title: "ALTER INDEX"
bookToc: true
---


# ALTER INDEX Statement

```SQL
ALTER INDEX [IF EXISTS] name ON table_name RENAME TO name
```

Rename a table index.

The **`ALTER INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER INDEX metrics_ts_idx ON metrics RENAME TO metrics_time_idx;
```
