---
weight: 4
title: "SHOW VIEWS"
bookToc: false
---

## SHOW VIEWS Statement

```SQL
SHOW VIEWS
```

Show views created in the system.

---

```SQL
create view test as select [1,2,3]

show views
[{
  "public.test": {
    "schema": "public",
    "name": "test",
    "query": "select [1,2,3]",
    "columns": []
  }
}]

select system.views()['public.test'].query
["select [1,2,3]"]

select *.schema, *.name from system.views()
[["public", "test"]]
```
