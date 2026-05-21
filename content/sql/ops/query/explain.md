---
weight: 4
title: EXPLAIN
bookToc: true
---

# EXPLAIN / PROFILE

```SQL
[EXPLAIN] [BEGIN;] statement; [...] [END;]
[PROFILE] [BEGIN;] statement; [...] [END;]
```

The **`EXPLAIN`** clause returns debug information about the transaction without executing it.

The **`PROFILE`** clause executes the transaction, measures the execution time, and returns the debug information.

Each transaction is compiled into two bytecode sections:

* **`main`** — commands for the distributed transaction coordination and results processing by the frontend session.
* **`pushdown`** — commands for data access and modification on one or many backend workers (per partition).

A **`Virtual Machine`** (VM) interprets bytecode until completion and produces an accessible result.
There are several VM contexts. One for the frontend (session) and one for each backend worker in the system.

Each session acts as a distributed transaction coordinator for backend workers.

---

```SQL
CREATE TABLE example (id int primary key);
EXPLAIN SELECT count(*) FROM example GROUP BY id;

explain
───────

main
  0   send_all            0      0      40    # amelie.example (select, closing)
  1   recv_aggs           1      0      32
  2   set                 2      1      0
  3   store_open          3      1      8
  4   count               4      3      0
  5   push                4      0      0
  6   set_add             2      0      0
  7   store_next          3      4      0
  8   free                3      0      0
  9   free                1      0      0
 10   ret                 2      0      -

pushdown
  0   set                 0      1      1
  1   table_open          1      0      8     # amelie.example (primary) part
  2   table_readi32       2      1      -     # id
  3   push                2      0      0
  4   set_get             2      0      0
  5   push_int            -      0      0     # 1
  6   set_agg             0      2      32
  7   table_next          1      2      0
  8   free                1      0      0
  9   ret                 0      0      -

access
  •   amelie.example shared [select]
```
