---
weight: 13
title: "Misc"
bookToc: true
---

# Misc Functions

### **`null error(string)`**

Generate an error.

```SQL
select error("error message");
```

---

### **`int identity_of(schema, name)`**

Get current serial value of the table identified by
the **`schema`** and **`name`**.

```SQL
CREATE TABLE example (id int primary key generated always as identity);
INSERT INTO example () VALUES (), (), ();
SELECT * FROM example;

id
──
0
1
2

SELECT identity_of("public", "example");

identity_of
───────────
3
```
