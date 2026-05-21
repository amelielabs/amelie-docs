---
weight: 15
title: 'NULL'
type: docs
bookToc: true
---

# NULL

**`NULL`** represents missing data and is technically not a type unless explicitly encoded inside a **`JSON`**.

Any operations with **`NULL`** values produce **`NULL`**.

Aggregate functions ignore **`NULL`** values.

---

```SQL
SELECT null as const;

const
─────
null

SELECT 1 + null as expr;

expr
────
null

SELECT {"data": null} as json;

json
────
{
  "data": null
}
```
