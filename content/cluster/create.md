---
weight: 2
title: "CREATE NODE"
bookToc: false
---

## CREATE NODE Statement

```SQL
CREATE [COMPUTE] NODE [IF NOT EXISTS] [id]
```

Create a new compute node.

If **`id`** is not provided, it will be generated automatically. Otherwise, it must be
presented in the format of **`UUID`**.

The new compute node will not be automatically assigned to the existing tables;
only new tables will start using it.

---

```SQL
create node "3a0803be-917f-6400-a5cb-3344f126a58b"

create compute node
```
