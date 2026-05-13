---
weight: 5
title: Strings
type: docs
bookToc: true
---

## String Expressions

Following string expressions are supported:

#### **`STRING`** only

* expr || expr

Any operation with **`NULL`** value produce **`NULL`**.

---

```SQL
select "hello " || "world!";
["hello world!"]
```
