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
select exists(select * from [])
[false]

select exists(select * from [1,2,3])
[true]
```
