---
weight: 14
title: EXISTS
type: docs
bookToc: false
---

## EXISTS operator

```SQL
EXISTS (expr)
```

**`EXISTS`** operator returns true if the expr subquery result has rows.

---

```SQL
select exists(select * from test)
[true]

select exists(select * from test limit 0)
[false]
```
