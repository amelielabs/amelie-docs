---
weight: 10
title: ANY / ALL
type: docs
bookToc: false
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
select 1 = any ([1,2,3]);
[true]

select 1 = any (select id from test);
[true]

select 1 = all (select id from test);
[false]
```
