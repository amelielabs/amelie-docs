---
weight: 2
title: Logical
type: docs
bookToc: false
---

## Logical Operations

Following basic logical operations are supported:

* **`NOT`** expr
* expr **`AND`** expr

---

```SQL
select not true
[false]

select true and true
[true]

select 0 and 1
[false]
```
