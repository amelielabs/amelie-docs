---
weight: 2
title: TINYINT
type: docs
bookToc: false
---

## TINYINT

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

* **`I8`**, **`INT8`**, **`TINYINT`**
  
  Defines `8bit` integer. The supported range is from **`-128`** to **`127`**.

---

```SQL
select 123
[123]
```

```SQL
create table test(id int8 primary key)
insert into test values (1), (2), (3)
select id from test
[1, 2, 3]
```

```SQL
create table test(id tinyint primary key serial, data int)
insert into test (data) values (1), (2), (3)
select * from test
[[0, 1], [1, 2], [2, 3]]
```
