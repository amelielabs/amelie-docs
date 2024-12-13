---
weight: 1
title: Arithmetical
type: docs
bookToc: false
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

* expr + expr
* expr - expr

#### **`VECTOR`** only

* expr + expr
* expr - expr
* expr * expr

Any operation with **`NULL`** value produce **`NULL`**.

---

```SQL
select 2 * 2;
[4]

select 2 + 3.14;
[5.14]

select current_timestamp - interval '5 hours';
["2024-09-26 12:12:10.684550+03"]

select [1.0, 2.1, 3]::vector * [1.5, 1.5, 1.5]::vector;
[1.5, 3.15, 4.5]
```
