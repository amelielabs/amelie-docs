---
weight: 11
title: EXPLAIN
type: docs
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

* The first one is for the distributed transaction coordination and results merging by the session
* The second one is for the actual data access and modification for each node individually

A **`Virtual Machine`** (VM) interprets bytecode until completion and produces an accessible result.
There are several VM contexts. One for each transaction coordinator and one for each compute node in the system.

---

```SQL
create table test (id int primary key)

explain select count(*) from test
[{
  "bytecode": {
    "coordinator": {
      "00": "send_all            0      0      -     # public.test",
      "01": "recv                0      0      0     ",
      "02": "merge_recv_agg      0      0      20    ",
      "03": "set                 1      1      0     ",
      "04": "store_open          1      0      6     ",
      "05": "jmp                 10     0      0     ",
      "06": "count               2      1      0     ",
      "07": "push                2      0      0     ",
      "08": "set_add             1      0      0     ",
      "09": "store_next          1      6      0     ",
      "10": "store_open          1      1      0     ",
      "11": "cte_set             0      1      0     ",
      "12": "content             0      -      -     ",
      "13": "ret                 0      0      0     "
    },
    "node": {
      "00": "set                 0      1      1     ",
      "01": "int                 1      -      0     # -2147483648",
      "02": "push                1      0      0     ",
      "03": "table_open          0      0      5     # public.test (primary)",
      "04": "jmp                 12     0      0     ",
      "05": "bool                1      1      0     ",
      "06": "push                1      0      0     ",
      "07": "set_get             1      0      0     ",
      "08": "int                 2      -      0     # 1",
      "09": "push                2      0      0     ",
      "10": "set_agg             0      1      20    ",
      "11": "table_next          0      5      0     ",
      "12": "table_close         0      0      0     ",
      "13": "bool                1      1      0     ",
      "14": "push                1      0      0     ",
      "15": "set_get             1      0      0     ",
      "16": "null                2      0      0     ",
      "17": "push                2      0      0     ",
      "18": "set_agg             0      1      20    ",
      "19": "result              0      0      0     ",
      "20": "ret                 0      0      0     "
    }
  }
}]
```

```SQL
profile select count(*) from test
[{
  "bytecode": {
    "coordinator": {
      "00": "send_all            0      0      -     # public.test",
      "01": "recv                0      0      0     ",
      "02": "merge_recv_agg      0      0      20    ",
      "03": "set                 1      1      0     ",
      "04": "store_open          1      0      6     ",
      "05": "jmp                 10     0      0     ",
      "06": "count               2      1      0     ",
      "07": "push                2      0      0     ",
      "08": "set_add             1      0      0     ",
      "09": "store_next          1      6      0     ",
      "10": "store_open          1      1      0     ",
      "11": "cte_set             0      1      0     ",
      "12": "content             0      -      -     ",
      "13": "ret                 0      0      0     "
    },
    "node": {
      "00": "set                 0      1      1     ",
      "01": "int                 1      -      0     # -2147483648",
      "02": "push                1      0      0     ",
      "03": "table_open          0      0      5     # public.test (primary)",
      "04": "jmp                 12     0      0     ",
      "05": "bool                1      1      0     ",
      "06": "push                1      0      0     ",
      "07": "set_get             1      0      0     ",
      "08": "int                 2      -      0     # 1",
      "09": "push                2      0      0     ",
      "10": "set_agg             0      1      20    ",
      "11": "table_next          0      5      0     ",
      "12": "table_close         0      0      0     ",
      "13": "bool                1      1      0     ",
      "14": "push                1      0      0     ",
      "15": "set_get             1      0      0     ",
      "16": "null                2      0      0     ",
      "17": "push                2      0      0     ",
      "18": "set_agg             0      1      20    ",
      "19": "result              0      0      0     ",
      "20": "ret                 0      0      0     "
    }
  },
  "profiler": {
    "time_run_ms": 0,
    "time_commit_ms": 0,
    "time_ms": 0,
    "sent_total": 3
  }
}]
```
