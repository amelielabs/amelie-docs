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
    "system": true
  },
  "public": {
    "name": "public",
    "system": true
  },
  "test": {
    "name": "test",
    "system": false
  }
}]

select system.schemas().public.system
[true]
```
