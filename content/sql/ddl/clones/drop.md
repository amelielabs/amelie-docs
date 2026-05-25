---
weight: 2
title: "DROP CLONE"
bookToc: true
---

# DROP CLONE

```SQL
DROP CLONE [IF EXISTS] name [CASCADE]
```

Drop table clone if it exists.

The **`DROP CLONE`** operation cannot be part of multi-statement transactions.

---

```SQL
DROP CLONE IF EXISTS docs_clone;
```
