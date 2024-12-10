---
weight: 13
title: 'NULL'
type: docs
bookToc: false
---

## NULL

**`NULL`** represents missing data and is technically not a type unless explicitly encoded inside a **`JSON`**.

Any operations with **`NULL`** values produce **`NULL`**.

Aggregate functions ignore **`NULL`** values.

---

```SQL
select null
[null]

select 1 + null
[null]

select {"data": null}
[{
  "data": null
}]
```

```SQL
create table test(id int primary key, data int)

insert into test values (1, null)
insert into test values (2, 48)
insert into test values (3, null)

select * from test
[[1, null], [2, 48], [3, null]]

select * from test where data is not null
[[2, 48]]

select count(data) from test
[1]

select count(*) from test where data = null
[2]

update test set data = id where data is null

select * from test
[[1, 1], [2, 48], [3, 3]]
```
