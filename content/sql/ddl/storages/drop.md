---
weight: 2
title: "DROP STORAGE"
bookToc: true
---

# DROP STORAGE

```SQL
DROP STORAGE [IF EXISTS] name
```

Drop storage object if it exists.

Storage must be not in use at the moment.

The **`DROP STORAGE`** operation cannot be part of multi-statement transactions.

---

```SQL
DROP STORAGE IF EXISTS ssd;
```
