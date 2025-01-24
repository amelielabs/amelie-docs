---
weight: 4
title: INT
type: docs
bookToc: false
---

## INT

**`INT`**, **`INTEGER`**, **`INT32`**, **`I32`** defines `32-bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-2147483648`** to **`2147483647`**.

---

```SQL
select 123;
[123]
```

```SQL
create table example (id int primary key);
insert into example values (1), (2), (3);
select id from example;
[1, 2, 3]
```

```SQL
create table example (id integer primary key as identity, data int);
insert into example (data) values (1), (2), (3);
select * from example;
[[0, 1], [1, 2], [2, 3]]
```
