---
weight: 2
title: TINYINT
type: docs
bookToc: true
---

# TINYINT

**`TINYINT`**, **`INT8`**, **`I8`** defines `8-bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-128`** to **`127`**.

---

```SQL
SELECT 123 as example;

example
───────
123
```

```SQL
CREATE TABLE example (id int primary key, data int8);
```
