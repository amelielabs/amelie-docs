---
weight: 3
title: Comparison
type: docs
bookToc: false
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
select 1 > 2;
[false]

select [1,2,3] = [1,2,3];
[true]

select {"id": 48} = {'id': 48};
[true]

select now() = now();
[true]

select now() = now()::int;
[true]

select now() - interval '1 hour' < now();
[true]
```
