---
weight: 2
title: TINYINT
type: docs
bookToc: false
---

## TINYINT

**`TINYINT`**, **`INT8`**, **`I8`** defines `8-bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-128`** to **`127`**.

---

```SQL
select 123;
[123]
```

```SQL
create table example (id tinyint primary key serial, data int);
insert into example (data) values (1), (2), (3);
select * from example;
[[0, 1], [1, 2], [2, 3]]
```

```SQL
create table example (id int8 primary key);
insert into example values (1), (2), (3);
select id from example;
[1, 2, 3]
```
