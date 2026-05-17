---
weight: 8
title: "Null"
bookToc: true
---

# Functions to work with NULL

### **`any coalesce(...)`**

Return a first non-null argument.

```SQL
SELECT coalesce(null, 1, null, 2);

coalesce
────────
1
```

---

### **`any nullif(a, b)`**

Return a **`null`** value if **`a`** equals **`b`**, otherwise, it returns **`a`**.

```SQL
SELECT nullif(1, 1);

nullif
──────
null
```
