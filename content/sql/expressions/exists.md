---
weight: 14
title: EXISTS
type: docs
bookToc: true
---

# EXISTS operator

```SQL
EXISTS (expr)
```

**`EXISTS`** operator returns true if the expr subquery result has rows.

---

```SQL
SELECT exists(select * from test) as query;

query
─────
true

SELECT exists(select * from test limit 0) as query;

query
─────
false
```
