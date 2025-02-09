---
weight: 4
title: "SHOW BACKENDS"
bookToc: false
---

## SHOW BACKENDS Statement

```SQL
SHOW BACKENDS [FORMAT type]
```

Show created and active backend workers in the system.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
show backends;
[{
  "id": "74f303a3-c434-fda7-59ca-bce4d9dca6a9"
}, {
  "id": "c5ec6e00-4a76-f47f-2f30-d617afc34fcd"
}, {
  "id": "f928a78a-3417-ffe1-356c-4ec069088558"
}, {
  "id": "da8ffa7f-ab01-5d19-f425-95999f566c6c"
}, {
  "id": "b56c9b73-6c85-c151-8534-26865833f1be"
}, {
  "id": "6762162a-c1d9-5427-b5fa-3ef9d50f4f06"
}, {
  "id": "46e4731e-8a92-7653-7d9d-1b95299ddd0b"
}, {
  "id": "5d0d5104-0615-7aeb-2ce8-b71cd5c72962"
}, {
  "id": "d683a637-bb1d-740b-83c3-4f9753a03085"
}, {
  "id": "f702818d-281f-7069-9eca-d50f78d0e6b1"
}, {
  "id": "e5971ded-2d9a-186e-7a0f-f1dd7897fe45"
}]

select system.backends()::size;
[11]

select id from system.backends();
["74f303a3-c434-fda7-59ca-bce4d9dca6a9", "c5ec6e00-4a76-f47f-2f30-d617afc34fcd",
 "f928a78a-3417-ffe1-356c-4ec069088558", "da8ffa7f-ab01-5d19-f425-95999f566c6c",
 "b56c9b73-6c85-c151-8534-26865833f1be", "6762162a-c1d9-5427-b5fa-3ef9d50f4f06",
 "46e4731e-8a92-7653-7d9d-1b95299ddd0b", "5d0d5104-0615-7aeb-2ce8-b71cd5c72962",
 "d683a637-bb1d-740b-83c3-4f9753a03085", "f702818d-281f-7069-9eca-d50f78d0e6b1",
 "e5971ded-2d9a-186e-7a0f-f1dd7897fe45"]
```
