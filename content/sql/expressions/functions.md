---
weight: 7
title: Functions / Methods
type: docs
bookToc: true
---

# Function and Method call

```SQL
[user.]function_name(arguments)

expr::[user.]function_name[(arguments)]
```

Amelie implements standard built-in functions for different purposes.
The call operator **`()`** is used to call a function. Each function has an associated schema.
If the schema is not defined, the function will be searched in the **`public`** schema.

Any function with one or more arguments can be executed in the format of the method using the **`::`** operator.
A method call is an alternative way to call a function. It automatically passes the left
expression result as the first argument to the function call, allowing functions to be called
in a chain one by one without nesting.

In the method call format, the parentheses **`()`** can be omitted if the function has only one argument.

---

```SQL
SELECT append([1,2,3], 4);

append
──────
[1, 2, 3, 4]

SELECT "2024-09-26 12:12:10.684550+03"::timestamp::int;

int
───
1727341930684550

SELECT [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector);

cos_distance
────────────
0.481455

UPDATE test SET data = data::append(4);
```
