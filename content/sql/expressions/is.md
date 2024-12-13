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

---

```SQL
select null is null;
[true]

select {"data": null}.data::type;
["json"]

select {"data": null}.data = null::json;
[true]
```
