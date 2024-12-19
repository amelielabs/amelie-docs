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

show tables;
[{
  "schema": "public",
  "name": "example",
  "shared": false
}]

show tables extended;
[{
  "schema": "public",
  "name": "example",
  "shared": false,
  "columns": [{
    "name": "id",
    "type": 2,
    "type_size": 4,
    "constraints": {
      "not_null": true,
      "serial": false,
      "random": false,
      "random_modulo": 9223372036854775807,
      "as_stored": "",
      "as_resolved": "",
      "default": null
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
    "id": 23,
    "node": "74f303a3-c434-fda7-59ca-bce4d9dca6a9",
    "min": 0,
    "max": 736
  }, {
    "id": 24,
    "node": "c5ec6e00-4a76-f47f-2f30-d617afc34fcd",
    "min": 736,
    "max": 1472
  }, {
    "id": 25,
    "node": "f928a78a-3417-ffe1-356c-4ec069088558",
    "min": 1472,
    "max": 2208
  }, {
    "id": 26,
    "node": "da8ffa7f-ab01-5d19-f425-95999f566c6c",
    "min": 2208,
    "max": 2944
  }, {
    "id": 27,
    "node": "b56c9b73-6c85-c151-8534-26865833f1be",
    "min": 2944,
    "max": 3680
  }, {
    "id": 28,
    "node": "6762162a-c1d9-5427-b5fa-3ef9d50f4f06",
    "min": 3680,
    "max": 4416
  }, {
    "id": 29,
    "node": "46e4731e-8a92-7653-7d9d-1b95299ddd0b",
    "min": 4416,
    "max": 5152
  }, {
    "id": 30,
    "node": "5d0d5104-0615-7aeb-2ce8-b71cd5c72962",
    "min": 5152,
    "max": 5888
  }, {
    "id": 31,
    "node": "d683a637-bb1d-740b-83c3-4f9753a03085",
    "min": 5888,
    "max": 6624
  }, {
    "id": 32,
    "node": "f702818d-281f-7069-9eca-d50f78d0e6b1",
    "min": 6624,
    "max": 7360
  }, {
    "id": 33,
    "node": "e5971ded-2d9a-186e-7a0f-f1dd7897fe45",
    "min": 7360,
    "max": 8096
  }]
}]

select name from system.tables();
["example"]

show table example;
[{
  "schema": "public",
  "name": "example",
  "shared": false
}]

select system.table('example').columns;
[[{
  "name": "primary",
  "type": 2,
  "unique": true,
  "primary": true,
  "keys": [{
    "column": 0
  }]
}]]
```
