---
weight: 11
title: IN
type: docs
bookToc: false
---

## IN operator

```SQL
expr [NOT] IN (expr, ...)
```

The **`IN`** operator returns true (or false in case of **`NOT`** clause usage) if its expression on the left matches any of
the expressions (including subqueries results) on the right.

---

```SQL
select 1 in (1,2,3)
[true]

select 1 in (select id from test)
[true]
```
