---
weight: 3
title: SMALLINT
type: docs
bookToc: false
---

## SMALLINT

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

* **`I16`**, **`INT16`**, **`SMALLINT`**

  Defines `16bit` integer. The supported range is from **`-32768`** to **`32767`**.

---

```SQL
select 123
[123]
```

```SQL
create table test(id int16 primary key)
insert into test values (1), (2), (3)
select id from test
[1, 2, 3]
```

```SQL
create table test(id smallint primary key serial, data int)
insert into test (data) values (1), (2), (3)
select * from test
[[0, 1], [1, 2], [2, 3]]
```
