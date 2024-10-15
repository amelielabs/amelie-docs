---
weight: 4
title: "SHOW SCHEMAS"
bookToc: false
---

## SHOW SCHEMAS Statement

```SQL
SHOW SCHEMAS
```

Show schema objects created in the system.

---

```SQL
create schema test

show schemas
[{
  "system": {
    "name": "system",
    "system": true,
    "create": false
  },
  "public": {
    "name": "public",
    "system": true,
    "create": true
  },
  "test": {
    "name": "test",
    "system": false,
    "create": true
  }
}]

select system.schemas().public.system
[true]

select name from system.schemas()
["system", "public", "test"]
```
