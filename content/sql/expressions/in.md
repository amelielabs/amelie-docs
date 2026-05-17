---
weight: 11
title: IN
type: docs
bookToc: true
---

## IN operator

```SQL
expr [NOT] IN (expr, ...)
```

The **`IN`** operator returns true (or false in case of **`NOT`** clause usage) if its expression on the left matches any of
the expressions (including subqueries results) on the right.

---

```SQL
SELECT 1 in (1,2,3) as expr;

expr
────
true

SELECT 1 in (select id from test) as query;

query
─────
true
```
