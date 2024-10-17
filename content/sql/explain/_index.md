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
      "00": "send_all            0      0      0     ",
      "01": "recv                0      0      0     ",
      "02": "group_merge_recv    0      0      0     ",
      "03": "set                 1      0      0     ",
      "04": "cursor_open_expr    1      0      6     ",
      "05": "jmp                 9      0      0     ",
      "06": "group_read_aggr     2      1      0     ",
      "07": "set_add             1      2      0     ",
      "08": "cursor_next         1      6      0     ",
      "09": "cursor_close        1      0      0     ",
      "10": "cte_set             0      1      0     ",
      "11": "body                0      0      0     ",
      "12": "ret                 0      0      0     "
    },
    "node": {
      "00": "group               0      0      0     ",
      "01": "group_add           0      0      -1    ",
      "02": "null                1      0      0     ",
      "03": "push                1      0      0     ",
      "04": "group_write         0      0      0     ",
      "05": "int_min             1      0      0     ",
      "06": "push                1      0      0     ",
      "07": "cursor_open         0      0      9     # public.test (primary)",
      "08": "jmp                 13     0      0     ",
      "09": "cursor_read         1      0      0     ",
      "10": "push                1      0      0     ",
      "11": "group_write         0      0      0     ",
      "12": "cursor_next         0      9      0     ",
      "13": "cursor_close        0      0      0     ",
      "14": "result              0      0      0     ",
      "15": "ret                 0      0      0     "
    }
  }
}]
```

```SQL
profile select count(*) from test
[{
  "bytecode": {
    "coordinator": {
      "00": "send_all            0      0      0     ",
      "01": "recv                0      0      0     ",
      "02": "group_merge_recv    0      0      0     ",
      "03": "set                 1      0      0     ",
      "04": "cursor_open_expr    1      0      6     ",
      "05": "jmp                 9      0      0     ",
      "06": "group_read_aggr     2      1      0     ",
      "07": "set_add             1      2      0     ",
      "08": "cursor_next         1      6      0     ",
      "09": "cursor_close        1      0      0     ",
      "10": "cte_set             0      1      0     ",
      "11": "body                0      0      0     ",
      "12": "ret                 0      0      0     "
    },
    "node": {
      "00": "group               0      0      0     ",
      "01": "group_add           0      0      -1    ",
      "02": "null                1      0      0     ",
      "03": "push                1      0      0     ",
      "04": "group_write         0      0      0     ",
      "05": "int_min             1      0      0     ",
      "06": "push                1      0      0     ",
      "07": "cursor_open         0      0      9     # public.test (primary)",
      "08": "jmp                 13     0      0     ",
      "09": "cursor_read         1      0      0     ",
      "10": "push                1      0      0     ",
      "11": "group_write         0      0      0     ",
      "12": "cursor_next         0      9      0     ",
      "13": "cursor_close        0      0      0     ",
      "14": "result              0      0      0     ",
      "15": "ret                 0      0      0     "
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
