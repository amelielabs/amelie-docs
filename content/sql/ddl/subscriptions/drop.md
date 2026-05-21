---
weight: 2
title: "DROP SUBSCRIPTION"
bookToc: true
---

# DROP SUBSCRIPTION

```SQL
DROP SUBSCRIPTION [IF EXISTS] name [CASCADE]
```

Drop subscription object if it exists.

The **`DROP SUBSCRIPTION`** operation cannot be part of multi-statement transactions.

---

```SQL
DROP SUBSCRIPTION IF EXISTS example_sub;
```
