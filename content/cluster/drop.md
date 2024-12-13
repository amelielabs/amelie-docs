---
weight: 3
title: "DROP NODE"
bookToc: false
---

## DROP NODE Statement

```SQL
DROP NODE [IF EXISTS] id
```

Shut down and remove existing compute now identified by **`id`**.

The compute node can only be removed if no table uses it.

---

```SQL
drop node "3a0803be-917f-6400-a5cb-3344f126a58b";
```
