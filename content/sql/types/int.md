---
weight: 1
title: INT
type: docs
bookToc: false
---

## INT

Defines an integer. The types **`INT`** and **`INTEGER`** are synonymous.

Both can be used in arithmetical operations. The supported range is from
**`-9223372036854775808`** to **`9223372036854775807`**. Type size is automatically encoded
based on its value.

Types can be used as a part of the primary or secondary key.

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
create table test(id int primary key serial, data int)
insert into test (data) values (1), (2), (3)
select * from test
[[0, 1], [1, 2], [2, 3]]
```
