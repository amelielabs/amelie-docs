---
weight: 16
title: '*'
type: docs
bookToc: false
---

## Star (*)

Amelie star **`*`** has an extended purpose compared to the traditional SQL.

Stars are used as references to the current row or object position of a scan and can be
used directly in expressions.

---

```SQL
select * from [1,2,3]
[1, 2, 3]

select count(*) from [1,2,3]
[3]

select * + 10 from [1,2,3]
[11, 12, 13]

select * from {"a": 1, "b": 2}
[1, 2]

select ** from {"a": 1, "b": 2}
["a", "b"]

select lambda obj({}) = obj::set("key" || *::string, *) from [1,2,3]
[{
  "key1": 1,
  "key2": 2,
  "key3": 3
}]
```

```SQL
create table test (id int primary key, data array)
insert into test values (1, [1,2,3])

select id, data from test
[[1, [1, 2, 3]]]

select *[0], *[1] from test
[[1, [1, 2, 3]]]
```
