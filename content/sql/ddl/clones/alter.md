---
weight: 3
title: "ALTER CLONE"
bookToc: true
---

# ALTER CLONE

```SQL
ALTER CLONE [IF EXISTS] name RENAME TO name
ALTER CLONE [IF EXISTS] name DESCRIPTION text
```

Change the definition of a table clone if it exists.

Currently, the **`ALTER CLONE`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER CLONE A RENAME TO B;
```
