---
weight: 2
title: "Aggregates"
bookToc: true
---

# Aggregate Functions

Amelie executes aggregate functions individually per backend in parallel.
After the successful execution, each computation's results (partial aggregates) are merged, processed, and returned.

Following aggregate functions are supported:

* **`count(distinct any)`**
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

There are also [Lambda Aggregates](/docs/sql/ops/query/lambda), a unique aggregate type to Amelie.

---

```SQL
CREATE TABLE example (id int primary key);
INSERT INTO example VALUES (1), (2), (3);
SELECT count(*), min(id), max(id), sum(id), avg(id) FROM example;

count  min  max  sum  avg
───────────────────────────
3      1    3    6    2
```
