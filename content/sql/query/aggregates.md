---
weight: 3
title: "Aggregates"
bookToc: false
---

## Partial Aggregates

Amelie executes aggregate functions individually per compute node in parallel.
After the successful execution, each computation's results are merged, processed, and returned.

Amelie supports the following aggregate functions:

* **`count(expr)`**
* **`sum(expr)`**
* **`avg(expr)`**
* **`min(expr)`**
* **`max(expr)`**

All functions ignore **`NULL`** values.

There are also [Lambda Aggregates](/docs/sql/query/lambda), a unique aggregate type to Amelie.

---

```SQL
create table test (id int primary key)
insert into test values (1), (2), (3)
select count(*), min(id), max(id), sum(id), avg(id) from test
[[3, 1, 3, 6, 2]]
select count(*) from [1, 2, null, 3]
[3]
```
