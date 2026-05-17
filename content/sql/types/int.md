---
weight: 4
title: INT
type: docs
bookToc: true
---

## INT

**`INT`**, **`INTEGER`**, **`INT32`**, **`I32`** defines `32-bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-2147483648`** to **`2147483647`**.

---

```SQL
SELECT 123 as example;

example
───────
123
```

```SQL
CREATE TABLE example (id integer primary key, data int);
```
