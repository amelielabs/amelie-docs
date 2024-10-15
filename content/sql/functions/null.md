---
weight: 5
title: "Null"
bookToc: false
---

## Functions to work with NULL

All functions are located in the **`public`** schema, which is default.

### coalesce(...)

Return a first non-null argument.

```SQL
select coalesce(null, 1, null, 2)
[1]
```

---

### nullif(a, b)

Return a **`null`** value if **`a`** equals **`b`**, otherwise, it returns **`a`**.

```SQL
select nullif(1, 1)
[null]
```
