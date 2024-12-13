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
select null;
[null]

select 1 + null;
[null]

select {"data": null};
[{
  "data": null
}]
```

```SQL
create table example (id int primary key, data int);

insert into example values (1, null);
insert into example values (2, 48);
insert into example values (3, null);

select * from example;
[[1, null], [2, 48], [3, null]]

select * from example where data is not null;
[[2, 48]]

select count(data) from example;
[1]

select count(*) from example where data = null;
[2]

update example set data = id where data is null;

select * from example;
[[1, 1], [2, 48], [3, 3]]
```
