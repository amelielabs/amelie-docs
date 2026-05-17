---
weight: 1
title: Arithmetical
type: docs
bookToc: true
---

## Arithmetical Expressions

Following arithmetical operations are supported:

#### **`INT, FLOAT, DOUBLE`**

* expr + expr
* expr - expr
* expr * expr
* expr / expr
* expr % expr

#### **`TIMESTAMP, INTERVAL`**

* timestamp + interval = timestamp
* timestamp - interval = timestamp
* timestamp - timestamp = interval

#### **`DATE, INT`**

* date + int = date
* date - int = date
* date - date = int (days)

#### **`DATE, INTERVAL`**

* date + interval = timestamp
* date - interval = timestamp

#### **`VECTOR`** only

* expr + expr
* expr - expr
* expr * expr

Any operation with **`NULL`** value produce **`NULL`**.

---

```SQL
SELECT 2 + 2 as expr;

expr
────
4

SELECT current_timestamp - interval '5 hours' as expr;

expr
────
2026-05-17 12:52:51.743287+03
```
