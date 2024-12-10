---
weight: 5
title: BIGINT
type: docs
bookToc: false
---

## BIGINT

All integer types are signed and can be used in arithmetical operations or as part of
the primary or secondary key.

* **`I64`**, **`INT64`**, **`BIGINT`**

  Defines `64bit` integer. The supported range is from **`-9223372036854775808`** to **`9223372036854775807`**.

---

```SQL
select 123
[123]
```

```SQL
create table test(id int64 primary key)
insert into test values (1), (2), (3)
select id from test
[1, 2, 3]
```

```SQL
create table test(id bigint primary key serial, data int)
insert into test (data) values (1), (2), (3)
select * from test
[[0, 1], [1, 2], [2, 3]]
```
