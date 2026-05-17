---
weight: 4
title: Bitwise
type: docs
bookToc: true
---

## Bitwise Operations

Following bitwise operations are supported:

#### **`INT`** only

* expr | expr
* expr & expr
* expr ^ expr
* expr << expr
* expr >> expr
* ~expr

Any operation with **`NULL`** value produce **`NULL`**.

---

```SQL
SELECT 1 << 4 as expr;

expr
────
16
```
