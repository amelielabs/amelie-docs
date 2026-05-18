---
weight: 2
title: "DROP INDEX"
bookToc: true
---

# DROP INDEX Statement

```SQL
DROP INDEX [IF EXISTS] name ON table_name
```

Drop table index.

The **`DROP INDEX`** operation cannot be part of multi-statement transactions.

---

```SQL
DROP INDEX metrics_ts_idx ON metrics;
```
