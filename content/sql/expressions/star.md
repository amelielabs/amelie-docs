---
weight: 16
title: '*'
type: docs
bookToc: false
---

## SELECT [alias.]*

Stars are used as a placeholder for all target columns in the **`SELECT`** statement.

---

```SQL
create table test (id int primary key)
insert into test values (1), (2), (3)
select * format 'json-obj' from test
[{"id": 1}, {"id": 2}, {"id": 3}]
```
