---
weight: 3
title: "CREATE USER"
bookToc: false
---

## CREATE USER Statement

```SQL
CREATE USER [IF NOT EXISTS] name [SECRET value]
```

Create a user identified by **`name`** if it does not exist with the optional **`SECRET`**.

---

```SQL
create user test;

show users;
[{
  "name": "test"
}]
```
