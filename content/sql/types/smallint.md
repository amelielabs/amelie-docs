---
weight: 3
title: SMALLINT
type: docs
bookToc: false
---

## SMALLINT

**`SMALLINT`**, **`INT16`**, **`I16`** defines `16bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-32768`** to **`32767`**.

---

```SQL
select 123;
[123]
```

```SQL
create table example (id smallint primary key serial, data int);
insert into example (data) values (1), (2), (3);
select * from example;
[[0, 1], [1, 2], [2, 3]]
```

```SQL
create table example (id int16 primary key);
insert into example values (1), (2), (3);
select id from example;
[1, 2, 3]
```
