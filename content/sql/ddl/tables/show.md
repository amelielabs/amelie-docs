---
weight: 4
title: "SHOW TABLES"
bookToc: false
---

## SHOW TABLES Statement

```SQL
SHOW TABLES
```

Show tables created in the system.

---

```SQL
create table test (id int primary key)

show tables
[{
  "public.test": {
    "schema": "public",
    "name": "test",
    "shared": false,
    "columns": [{
      "name": "id",
      "type": "int",
      "constraint": {
        "not_null": true,
        "generated": 0,
        "modulo": 9223372036854775807,
        "default": null
      }
    }],
    "indexes": [{
      "name": "primary",
      "type": 2,
      "unique": true,
      "primary": true,
      "keys": [{
        "ref": 0,
        "type": "int",
        "path": ""
      }]
    }],
    "partitions": [{
      "id": 23,
      "node": "69a4d13c-5977-7ef3-8e39-89ba9905bf99",
      "min": 0,
      "max": 736
    }, {
      "id": 24,
      "node": "1b8d1aeb-7128-de49-8f1e-64251002b165",
      "min": 736,
      "max": 1472
    }, {
      "id": 25,
      "node": "3f63ddba-60b9-ddae-a2cf-eb25df5d9d3b",
      "min": 1472,
      "max": 2208
    }, {
      "id": 26,
      "node": "61d24724-1795-a5cf-d6ff-01dd245b5666",
      "min": 2208,
      "max": 2944
    }, {
      "id": 27,
      "node": "c426f4c0-3ce1-0ba1-1af7-8dbb0e3ed93a",
      "min": 2944,
      "max": 3680
    }, {
      "id": 28,
      "node": "1078dd91-21b8-723c-c787-fbd1c7468869",
      "min": 3680,
      "max": 4416
    }, {
      "id": 29,
      "node": "4cdc5f85-ba26-e902-f976-91b0d6c241c6",
      "min": 4416,
      "max": 5152
    }, {
      "id": 30,
      "node": "10984861-f867-991c-2f93-de449ce484fb",
      "min": 5152,
      "max": 5888
    }, {
      "id": 31,
      "node": "23ee0716-8d66-167f-c760-9b20fbaa1bf7",
      "min": 5888,
      "max": 6624
    }, {
      "id": 32,
      "node": "0a780a21-78b7-19bc-b2d2-766f2247c9d8",
      "min": 6624,
      "max": 7360
    }, {
      "id": 33,
      "node": "558a2971-60b6-ec06-c8ae-c9c0b5973a2d",
      "min": 7360,
      "max": 8096
    }]
  }
}]

select system.tables()::type
["object"]

select system.tables()['public.test'].indexes
[{
  "name": "primary",
  "type": 2,
  "unique": true,
  "primary": true,
  "keys": [{
    "ref": 0,
    "type": "int",
    "path": ""
  }]
}]

select *.schema, *.name from system.tables()
[["public", "test"]]

select count(*), min(*.min), max(*.max) from system.tables()['public.test'].partitions
[[11, 0, 8096]]
```
