---
weight: 5
title: BIGINT
type: docs
bookToc: false
---

## BIGINT

**`BIGINT`**, **`INT64`**, **`I64`** defines `64bit` integer.

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

The supported range is from **`-9223372036854775808`** to **`9223372036854775807`**.

---

```SQL
select 123;
[123]
```

```SQL
create table example (id bigint primary key serial, data int);
insert into example (data) values (1), (2), (3);
select * from example;
[[0, 1], [1, 2], [2, 3]]
```

```SQL
create table example (id int64 primary key);
insert into example values (1), (2), (3);
select id from example;
[1, 2, 3]
```
