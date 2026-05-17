---
weight: 3
title: Comparison
type: docs
bookToc: true
---

## Comparison

The following operations of comparison are supported:

#### **`INT, FLOAT, DOUBLE, BOOL`**
* expr = expr
* expr <> expr
* expr > expr
* expr >= expr
* expr < expr
* expr <= expr

#### **`INT, TIMESTAMP, DATE`**

* expr = expr
* expr <> expr
* expr > expr
* expr >= expr
* expr < expr
* expr <= expr

#### **`INTERVAL`** only

* expr = expr
* expr <> expr
* expr > expr
* expr >= expr
* expr < expr
* expr <= expr

#### **`VECTOR`** only

* expr = expr
* expr <> expr
* expr > expr
* expr >= expr
* expr < expr
* expr <= expr

#### **`STRING`** only

* expr = expr
* expr <> expr

#### **`JSON`** only

* expr = expr
* expr <> expr

#### **`UUID`** only

* expr = expr
* expr <> expr
* expr > expr
* expr >= expr
* expr < expr
* expr <= expr

Any operation with **`NULL`** value produce **`NULL`**.

---

```SQL
SELECT 1 > 2 as expr;

expr
────
false

SELECT [1,2,3] = [1,2,3] as expr;

expr
────
true

SELECT now() - interval '1 hour' < now() as expr;

expr
────
true
```
