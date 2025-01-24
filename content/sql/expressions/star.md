---
weight: 17
title: '*'
type: docs
bookToc: false
---

## SELECT [alias.]*

Stars are used as a placeholder for all target columns in the **`SELECT`** statement.

---

```SQL
create table example (id int primary key);
insert into example values (1), (2), (3);
select * format 'json-obj' from example;
[{"id": 1}, {"id": 2}, {"id": 3}]
```
