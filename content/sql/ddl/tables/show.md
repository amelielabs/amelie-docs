---
weight: 4
title: "SHOW TABLE"
bookToc: false
---

## SHOW TABLE Statement

```SQL
SHOW TABLES [IN | FROM schema] [EXTENDED] [FORMAT type]
SHOW TABLE [schema.]name [IN | FROM schema] [EXTENDED] [FORMAT type]
```

Show tables created in the system.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
create table example (id int primary key);

show tables
[{
  "schema": "public",
  "name": "example",
  "unlogged": false
}]

show tables extended;
[{
  "schema": "public",
  "name": "example",
  "unlogged": false,
  "columns": [{
    "name": "id",
    "type": 2,
    "type_size": 4,
    "constraints": {
      "not_null": true,
      "random": false,
      "random_modulo": 9223372036854775807,
      "default": null,
      "as_identity": false,
      "as_stored": "",
      "as_resolved": ""
    }
  }],
  "indexes": [{
    "name": "primary",
    "type": 2,
    "unique": true,
    "primary": true,
    "keys": [{
      "column": 0
    }]
  }],
  "partitions": [{
    "id": 1,
    "backend": "7caf3275-0b59-2b42-6fe2-451efc5c24a2",
    "min": 0,
    "max": 1012
  }, {
    "id": 2,
    "backend": "2640f362-41e4-fcd4-c16f-40c3cd55c305",
    "min": 1012,
    "max": 2024
  }, {
    "id": 3,
    "backend": "4f3d12d4-0254-82bd-eadd-a9ca32c0f588",
    "min": 2024,
    "max": 3036
  }, {
    "id": 4,
    "backend": "49b8a424-b522-f5dc-6b47-5362ff0e996b",
    "min": 3036,
    "max": 4048
  }, {
    "id": 5,
    "backend": "ab157a15-3b52-7215-16fe-3189a960ef5b",
    "min": 4048,
    "max": 5060
  }, {
    "id": 6,
    "backend": "2529a2c3-10b0-f03a-a964-18c77a5022b8",
    "min": 5060,
    "max": 6072
  }, {
    "id": 7,
    "backend": "7dfd1314-3adf-21e4-fe5b-e1a00bbfa312",
    "min": 6072,
    "max": 7084
  }, {
    "id": 8,
    "backend": "d2703aed-37b2-599c-b33a-f857f72d3708",
    "min": 7084,
    "max": 8096
  }]
}]

select name from system.tables();
["example"]

show table example;
[{
  "schema": "public",
  "name": "example",
  "unlogged": false
}]

select system.table('example').columns;
[[{
  "name": "id",
  "type": 2,
  "type_size": 4,
  "constraints": {
    "not_null": true,
    "random": false,
    "random_modulo": 9223372036854775807,
    "default": null,
    "as_identity": false,
    "as_stored": "",
    "as_resolved": ""
  }
}]]
```
