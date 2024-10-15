---
weight: 9
title: "SHOW REPL"
bookToc: false
---

## SHOW REPL Statement

```SQL
SHOW REPLICATION
SHOW REPL
```

Get the replication status.

---

```SQL
show repl
[{
  "active": true,
  "role": "replica",
  "primary": "00000000-0000-0000-0000-000000000000"
}]

select system.repl().active
[true]
```
