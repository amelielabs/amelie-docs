---
weight: 9
title: IS
type: docs
bookToc: false
---

## IS operator

```SQL
expr IS [NOT] NULL
```

**`IS`** operator returns true (or false in case of **`NOT`** clause usage) if the
expression result is **`NULL`**.

Unlike traditional SQL, this operation is identical to direct comparison with
**`NULL`** using **`=`** or **`<>`** operators.

---

```SQL
select {"data": null}.data is null
[true]

select {"data": null}.data = null
[true]

select {"data": 123}.data <> null
[true]
```
