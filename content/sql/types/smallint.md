---
weight: 3
title: SMALLINT
type: docs
bookToc: true
---

# SMALLINT

**`SMALLINT`**, **`INT16`**, **`I16`** defines `16-bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-32768`** to **`32767`**.

---

```SQL
SELECT 123 as example;

example
───────
123
```

```SQL
CREATE TABLE example (id int primary key, data int16);
```
