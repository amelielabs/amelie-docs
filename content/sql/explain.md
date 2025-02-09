---
weight: 11
title: EXPLAIN
bookToc: false
---

## EXPLAIN / PROFILE Statements

```SQL
[EXPLAIN] [BEGIN;] statement; [...] [COMMIT;]
[PROFILE] [BEGIN;] statement; [...] [COMMIT;]
```

The **`EXPLAIN`** clause returns debug information about the transaction without executing it.

The **`PROFILE`** clause executes the transaction, measures the execution time, and returns the debug information.

Each transaction is compiled into two bytecode sections:

* Frontend — commands for the distributed transaction coordination and results processing by the frontend session.
* Backend — commands for data access and modification on one or many backend workers.

A **`Virtual Machine`** (VM) interprets bytecode until completion and produces an accessible result.
There are several VM contexts. One for the frontend (session) and one for each backend worker in the system.

Each session acts as a distributed transaction coordinator for backend workers.

---

```SQL
create table example (id int primary key);

explain select count(*) from example group by id;
[{
  "bytecode": {
    "frontend": {
      "00": "send_all            0      0      -     # public.example",
      "01": "recv                0      0      0     ",
      "02": "bool                0      1      0     ",
      "03": "push                0      0      0     ",
      "04": "union_recv          0      -1     -1    ",
      "05": "union_set_aggs      0      24     0     ",
      "06": "set                 1      1      0     ",
      "07": "store_open          1      0      12    ",
      "08": "count               2      1      0     ",
      "09": "push                2      0      0     ",
      "10": "set_add             1      0      0     ",
      "11": "store_next          1      8      0     ",
      "12": "store_close         1      1      0     ",
      "13": "cte_set             0      1      0     ",
      "14": "content             0      -      -     ",
      "15": "ret                 0      0      0     "
    },
    "backend": {
      "00": "set_ordered         0      1      1     ",
      "01": "table_open          0      1      9     # public.example (primary)",
      "02": "table_readi32       1      0      0     ",
      "03": "push                1      0      0     ",
      "04": "set_get             1      0      0     ",
      "05": "int                 2      -      0     # 1",
      "06": "push                2      0      0     ",
      "07": "set_agg             0      1      24    ",
      "08": "table_next          0      2      0     ",
      "09": "table_close         0      0      0     ",
      "10": "set_sort            0      0      0     ",
      "11": "result              0      0      0     ",
      "12": "ret                 0      0      0     "
    }
  }
}]
```
