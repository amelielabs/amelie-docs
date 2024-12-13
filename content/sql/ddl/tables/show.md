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
create table example (id int primary key);

show tables;
[{
  "public.example": {
    "schema": "public",
    "name": "example",
    "shared": false,
    "columns": [{
      "name": "id",
      "type": 2,
      "type_size": 4,
      "constraint": {
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
      "id": 50,
      "node": "8ce9b211-8624-ed5d-c9d2-241c78f16f9a",
      "min": 0,
      "max": 736
    }, {
      "id": 51,
      "node": "26e5e42a-67ca-5d6c-6c1b-1bf8116943a8",
      "min": 736,
      "max": 1472
    }, {
      "id": 52,
      "node": "22a57593-2ccb-98eb-3321-b2816b9fb4ac",
      "min": 1472,
      "max": 2208
    }, {
      "id": 53,
      "node": "1c34c0b1-da70-2623-0217-ab2f102b5116",
      "min": 2208,
      "max": 2944
    }, {
      "id": 54,
      "node": "36064abc-fe69-d214-0e53-9c5e3b3e8160",
      "min": 2944,
      "max": 3680
    }, {
      "id": 55,
      "node": "8b5f91bd-c6d2-bd84-f3b4-e76b51f8af00",
      "min": 3680,
      "max": 4416
    }, {
      "id": 56,
      "node": "2bad7851-4522-2b3e-cd42-e34a59d9630e",
      "min": 4416,
      "max": 5152
    }, {
      "id": 57,
      "node": "a90bd338-691a-e0e9-50d1-8524fda1ac61",
      "min": 5152,
      "max": 5888
    }, {
      "id": 58,
      "node": "e7f15ffe-5463-8ba4-e12d-d636c43941db",
      "min": 5888,
      "max": 6624
    }, {
      "id": 59,
      "node": "182bcbe3-0afe-0e91-4b14-68c1584c276c",
      "min": 6624,
      "max": 7360
    }, {
      "id": 60,
      "node": "baa1f250-c164-ca4e-c1e2-2469a7b93067",
      "min": 7360,
      "max": 8096
    }]
  }
}]

select system.tables()['public.example'].indexes;
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
