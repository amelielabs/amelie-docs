---
weight: 2
title: Logical
type: docs
bookToc: true
---

# Logical Operations

Following basic logical operations are supported:

* **`NOT`** expr
* expr **`AND`** expr

---

```SQL
SELECT not true as expr;

expr
────
false

SELECT true and true as expr;

expr
────
true

SELECT 0 and 1 as expr;

expr
────
false
```
