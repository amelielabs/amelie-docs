---
weight: 3
title: "ALTER BRANCH"
bookToc: true
---

# ALTER BRANCH

```SQL
ALTER BRANCH [IF EXISTS] name RENAME TO name
```

Change the definition of a branch if it exists.

Currently, the **`ALTER BRANCH`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER BRANCH A RENAME TO B;
```
