---
weight: 10
title: ANY / ALL
type: docs
bookToc: true
---

## ANY / ALL operator

```SQL
expr operator ANY (expr)
expr operator ALL (expr)
```

**`ANY`** returns true if its operator result is true to any of the elements in the expression.
**`ALL`** returns true if its operator result is true to all the elements in the expression.

Supported **`operators`** are: **`=`**, **`>`**, **`>=`**, **`<`**, **`<=`**.

The expression must be either **`JSON array`** or **`Subquery`**.

---

```SQL
SELECT 1 = any ([1,2,3]) as expr;

expr
────
true

SELECT 1 = any (select id from test) as query;

query
─────
true

SELECT 1 = all (select id from test) as query;

query
─────
false
```
