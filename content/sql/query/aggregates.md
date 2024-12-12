---
weight: 3
title: "Aggregates"
bookToc: false
---

## Aggregate Functions

Amelie executes aggregate functions individually per compute node in parallel.
After the successful execution, each computation's results (partial aggregates) are merged, processed, and returned.

Following aggregate functions are supported:

* **`count(any)`**
* **`sum(int)`**
* **`sum(double)`**
* **`avg(int)`**
* **`avg(double)`**
* **`min(int)`**
* **`min(double)`**
* **`max(int)`**
* **`max(double)`**

All functions ignore **`NULL`** values.

There are also [Lambda Aggregates](/docs/sql/query/lambda), a unique aggregate type to Amelie.

---

```SQL
create table test (id int primary key)
insert into test values (1), (2), (3)
select count(*), min(id), max(id), sum(id), avg(id) from test
[[3, 1, 3, 6, 2]]
```
