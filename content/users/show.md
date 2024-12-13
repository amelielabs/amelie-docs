---
weight: 6
title: "SHOW USERS"
bookToc: false
---

## SHOW USERS Statement

```SQL
SHOW USERS
```

Show all users defined in the system.

---

```SQL
create user test;

show users;
[{
  "test": {
    "name": "test"
  }
}]

select system.users().test;
[{
  "name": "test"
}]
```
