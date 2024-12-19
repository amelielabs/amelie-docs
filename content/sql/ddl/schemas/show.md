---
weight: 4
title: "SHOW SCHEMA"
bookToc: false
---

## SHOW SCHEMA Statement

```SQL
SHOW SCHEMAS [EXTENDED] [FORMAT type]
SHOW SCHEMA name [EXTENDED] [FORMAT type]
```

Show information about all or one schema.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
create schema example;

show schemas;
[{
  "name": "system",
  "system": true
}, {
  "name": "public",
  "system": true
}, {
  "name": "example",
  "system": false
}]

select name from system.schemas();
["system", "public", "example"]

show schema example;
[{
  "name": "example",
  "system": false
}]

select system.schema('example').system;
[false]
```
