---
weight: 4
title: "SHOW NODES"
bookToc: false
---

## SHOW NODES Statement

```SQL
SHOW NODES
```

Show created and active compute nodes in the system.

---

```SQL
show nodes
[{
  "5224e75c-4436-1f92-fd1c-2ea48fd086ec": {
    "id": "5224e75c-4436-1f92-fd1c-2ea48fd086ec",
    "compute": true
  },
  "63e7cadc-401f-3397-d9ca-6bb83a85522c": {
    "id": "63e7cadc-401f-3397-d9ca-6bb83a85522c",
    "compute": true
  },
  "a59a6d75-0534-773c-ae6c-520347e996e3": {
    "id": "a59a6d75-0534-773c-ae6c-520347e996e3",
    "compute": true
  },
  "029c29d2-1c32-c620-acc8-8af3100d5c5b": {
    "id": "029c29d2-1c32-c620-acc8-8af3100d5c5b",
    "compute": true
  },
  "a8dc2582-e5c9-30ec-ea8f-740452941231": {
    "id": "a8dc2582-e5c9-30ec-ea8f-740452941231",
    "compute": true
  },
  "20c70448-74af-b71a-1bb4-5e395dd04e11": {
    "id": "20c70448-74af-b71a-1bb4-5e395dd04e11",
    "compute": true
  },
  "a23b7fda-5652-8e86-98c2-1bf7fc055ed4": {
    "id": "a23b7fda-5652-8e86-98c2-1bf7fc055ed4",
    "compute": true
  },
  "08bfd8e1-463e-3c30-d18b-95bace40ab8b": {
    "id": "08bfd8e1-463e-3c30-d18b-95bace40ab8b",
    "compute": true
  },
  "9a04d955-9387-730c-d6f9-228ee318436e": {
    "id": "9a04d955-9387-730c-d6f9-228ee318436e",
    "compute": true
  },
  "c86d4fd0-7815-ac3e-52d2-59093217b91a": {
    "id": "c86d4fd0-7815-ac3e-52d2-59093217b91a",
    "compute": true
  },
  "00d07853-94d7-8fb5-63a6-3f7ed08638db": {
    "id": "00d07853-94d7-8fb5-63a6-3f7ed08638db",
    "compute": true
  }
}]

select system.nodes()::size
[11]

select system.nodes()['00d07853-94d7-8fb5-63a6-3f7ed08638db']
[{
  "id": "00d07853-94d7-8fb5-63a6-3f7ed08638db",
  "compute": true
}]

select system.nodes()::has('00d07853-94d7-8fb5-63a6-3f7ed08638db')
[true]

select id from system.nodes()
["5224e75c-4436-1f92-fd1c-2ea48fd086ec", "63e7cadc-401f-3397-d9ca-6bb83a85522c",
 "a59a6d75-0534-773c-ae6c-520347e996e3", "029c29d2-1c32-c620-acc8-8af3100d5c5b",
 "a8dc2582-e5c9-30ec-ea8f-740452941231", "20c70448-74af-b71a-1bb4-5e395dd04e11",
 "a23b7fda-5652-8e86-98c2-1bf7fc055ed4", "08bfd8e1-463e-3c30-d18b-95bace40ab8b",
 "9a04d955-9387-730c-d6f9-228ee318436e", "c86d4fd0-7815-ac3e-52d2-59093217b91a",
 "00d07853-94d7-8fb5-63a6-3f7ed08638db"]
```
