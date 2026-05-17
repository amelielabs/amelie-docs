---
weight: 9
title: IS
type: docs
bookToc: true
---

## IS operator

```SQL
expr IS [NOT] NULL
```

**`IS`** operator returns true (or false in case of **`NOT`** clause usage) if the
expression result is **`NULL`**.

---

```SQL
SELECT null is null as expr;

expr
────
true

SELECT {"data": null}.data::type;

type
────
json

SELECT {"data": null}.data = null::json as expr;

expr
────
true
```
