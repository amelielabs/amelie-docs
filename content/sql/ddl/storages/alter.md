---
weight: 3
title: "ALTER STORAGE"
bookToc: true
---

# ALTER STORAGE Statement

```SQL
ALTER STORAGE [IF EXISTS] name RENAME TO name
```

Change the definition of a storage if it exists.

Currently, the **`ALTER STORAGE`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER STORAGE ssd RENAME TO ssd2;
```
