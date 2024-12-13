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
create schema example;

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
  "example": {
    "name": "example",
    "system": false
  }
}]

select system.schemas().public.system;
[true]
```
