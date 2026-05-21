---
weight: 5
title: BIGINT
type: docs
bookToc: true
---

# BIGINT

**`BIGINT`**, **`INT64`**, **`I64`** defines `64-bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-9223372036854775808`** to **`9223372036854775807`**.

---

```SQL
SELECT 123 as example;

example
───────
123
```

```SQL
CREATE TABLE example (id int64 primary key);
```
