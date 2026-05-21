---
weight: 16
title: CAST
type: docs
bookToc: true
---

# CAST operator

```SQL
CAST (expr AS type)
```

**`CAST`** operator is used to convert the **`expression`** from one type to another.

**`CAST`** implemented as an alias to the [casting](/docs/sql/builtin/casting) functions.

---

```SQL
SELECT cast('1234' as int);

int
───
1234

SELECT cast("2024-09-26 12:12:10.684550+03" as timestamp);

timestamp
─────────
2024-09-26 12:12:10.684550+03

SELECT cast({"data": [1,2,3]} as string);

string
──────
{"data": [1, 2, 3]}
```
