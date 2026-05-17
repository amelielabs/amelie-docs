---
weight: 8
title: BETWEEN
type: docs
bookToc: true
---

## BETWEEN operator

```SQL
expr [NOT] BETWEEN a AND b
```

The **`BETWEEN`** operator returns true if its left expression result is between the results
of two other expressions on the right (a and b).

Comparison is inclusive, and identical to:

``` SQL
expr >= a AND expr <= b
```

**`BETWEEN`** operator accepts values as consts of the following types: **`INT`**, **`FLOAT`**, **`DOUBLE`**, **`STRING`**, **`INTERVAL`**, **`TIMESTAMP`** and **`DATE`**.

**`BETWEEN`** operator can be used to define range scan start/stop keys ([SELECT FROM WHERE](/docs/sql/ops/query/select)).

---

```SQL
SELECT 3 between 1 and 3 as expr;

expr
────
true
```
