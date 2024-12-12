---
weight: 5
title: "ALTER USER"
bookToc: false
---

## ALTER USER Statement

```SQL
ALTER USER name SECRET expr
```

Change the user secret.

---

```SQL
create user test
alter user test secret "secret"

show users
[{
  "name": "test"
}]
```
