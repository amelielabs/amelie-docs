---
weight: 13
title: LIKE
type: docs
bookToc: true
---

## LIKE operator

```SQL
expr [NOT] LIKE pattern
```

The **`LIKE`** operator returns true (or false in case of **`NOT`** clause usage) if
the string expression on the left matches the **`pattern`**.

The **`pattern`** is a regular string with two special characters used for templating:

* **`_`** match any single character
* **`%`** match zero, one or multiple characters

Escape characters can be used to match template characters.

---

```SQL
SELECT 'http://google.com' like '%google%' as expr;

expr
────
true

SELECT 'http://google.com'::like('%google%');

like
────
true
```
