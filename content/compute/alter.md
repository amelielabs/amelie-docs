---
weight: 2
title: "ALTER COMPUTE"
bookToc: false
---

## ALTER COMPUTE Statement

```SQL
ALTER COMPUTE [POOL] ADD  [NODE] [id]
ALTER COMPUTE [POOL] DROP [NODE] id
```

Add or remove compute node.

If **`id`** is not provided, it will be generated automatically. Otherwise, it must be
presented in the format of **`UUID`**.

The new compute node will not be automatically assigned to the existing tables;
only new tables will start using it.

The compute node can only be removed if no table uses it.

---

```SQL
alter compute add;
alter compute add "3a0803be-917f-6400-a5cb-3344f126a58b";
alter compute drop "3a0803be-917f-6400-a5cb-3344f126a58b";
```
