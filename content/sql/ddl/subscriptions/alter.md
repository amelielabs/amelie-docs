---
weight: 3
title: "ALTER SUBSCRIPTION"
bookToc: true
---

# ALTER SUBSCRIPTION

```SQL
ALTER SUBSCRIPTION [IF EXISTS] name RENAME TO name
```

Change the definition of a subscription if it exists.

Currently, the **`ALTER SUBSCRIPTION`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER SUBSCRIPTION example_sub RENAME TO example_sub_prev;
```
