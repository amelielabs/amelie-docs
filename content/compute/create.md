---
weight: 2
title: "CREATE BACKEND"
bookToc: false
---

## CREATE BACKEND Statement

```SQL
CREATE BACKEND [IF NOT EXISTS] [id]
```

Create new backend worker.

If **`id`** is not provided, it will be generated automatically. Otherwise, it must be
presented in the format of **`UUID`**.

The new backend worker will not be automatically assigned to the existing tables;
only new tables will start using it.

---

```SQL
create backend;
create backend "3a0803be-917f-6400-a5cb-3344f126a58b";
drop backend "3a0803be-917f-6400-a5cb-3344f126a58b";
```
