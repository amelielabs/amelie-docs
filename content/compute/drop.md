---
weight: 3
title: "DROP BACKEND"
bookToc: false
---

## DROP BACKEND Statement

```SQL
DROP BACKEND [IF EXISTS] id
```

Drop a backend worker.

The **`id`** must be presented in the format of **`UUID`**.

A backend worker can be dropped only if it has no associated partitions (tables).

---

```SQL
drop backend "3a0803be-917f-6400-a5cb-3344f126a58b";
```
