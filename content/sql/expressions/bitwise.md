---
weight: 4
title: Bitwise
type: docs
bookToc: false
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
select 1 << 4;
[16]
```
