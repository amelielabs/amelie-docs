---
weight: 13
title: "Misc"
bookToc: false
---

## Misc Functions

All functions are located in the **`public`** schema, which is default.

---

### **`null error(string)`**

Generate an error.

```SQL
select error("error message");
{"code": 1, "msg": "error message"}
```

---

### **`int serial(schema, name)`**

Get current serial value of the table identified by
the **`schema`** and **`name`**.

```SQL
create table example (id int primary key serial);
insert into example () values (), (), ();
select * from example;
[[0], [1], [2]]
select serial("public", "example");
[3]
```
