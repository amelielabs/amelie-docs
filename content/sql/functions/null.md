---
weight: 8
title: "Null"
bookToc: false
---

## Functions to work with NULL

All functions are located in the **`public`** schema, which is default.

---

### **`any coalesce(...)`**

Return a first non-null argument.

```SQL
select coalesce(null, 1, null, 2);
[1]
```

---

### **`any nullif(a, b)`**

Return a **`null`** value if **`a`** equals **`b`**, otherwise, it returns **`a`**.

```SQL
select nullif(1, 1);
[null]
```
