---
weight: 3
title: "ALTER FUNCTION"
bookToc: true
---

# ALTER FUNCTION

```SQL
ALTER FUNCTION [IF EXISTS] name RENAME TO name
ALTER FUNCTION [IF EXISTS] name DESCRIPTION text
```

Change the definition of a function if it exists.

Currently, the **`ALTER FUNCTION`** operation cannot be part of multi-statement transactions.

---

```SQL
ALTER FUNCTION example RENAME TO example_prev;
```
