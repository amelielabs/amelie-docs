---
weight: 13
title: "Misc"
bookToc: false
---

## Misc Functions

All functions are located in the **`public`** schema, which is default.

### error(string)

Generate an error.

```SQL
select error("error message")
{"code": 1, "msg": "error message"}
```

---

### serial(schema, name)

Get current serial value of the table identified by
the **`schema`** and **`name`**.

```SQL
create table test (id int primary key serial)
insert into test () values (), (), ()
select * from test
[[0], [1], [2]]
select serial("public", "test")
[3]
```
