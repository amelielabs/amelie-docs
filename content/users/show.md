---
weight: 6
title: "SHOW USER"
bookToc: false
---

## SHOW USER Statement

```SQL
SHOW USERS [FORMAT type]
SHOW USER name [FORMAT type]
```

Show users defined in the system.

The [FORMAT](/docs/sql/query/format) clause can be used to specify the format of the result.

---

```SQL
create user test;

show users;
[{
  "name": "test"
}]

select name from system.users();
["test"]

show user test;
[{
  "name": "test"
}]

select system.user('test').name;
["test"]
```
