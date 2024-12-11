---
weight: 4
title: INT
type: docs
bookToc: false
---

## INT

**`INT`**, **`INTEGER`**, **`INT32`**, **`I32`** defines `32bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-2147483648`** to **`2147483647`**.

---

```SQL
select 123
[123]
```

```SQL
create table test(id int primary key)
insert into test values (1), (2), (3)
select id from test
[1, 2, 3]
```

```SQL
create table test(id integer primary key serial, data int)
insert into test (data) values (1), (2), (3)
select * from test
[[0, 1], [1, 2], [2, 3]]
```
