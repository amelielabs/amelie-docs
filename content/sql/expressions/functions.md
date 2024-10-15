---
weight: 7
title: Functions / Methods
type: docs
bookToc: false
---

## Function and Method call

```SQL
[schema.]function_name(arguments)

expr::[schema.]function_name[(arguments)]
```

Amelie implements standard built-in functions for different purposes.
The call operator **`()`** is used to call a function. Each function has an associated schema.

Any function with one or more arguments can be executed in the format of the method using the **`::`** operator.
A method call is an alternative way to call a function. It automatically passes the left
expression result as the first argument to the function call, allowing functions to be called
in a chain one by one without nesting.

In the method call format, the parentheses **`()`** can be omitted if a function has only one argument.

---

```SQL
select append([1,2,3], 4)
[1,2,3,4]

select [1,2,3]::public.append(4)
[1,2,3,4]

update test set data = data::append(4) where id = 1

select "2024-09-26 12:12:10.684550+03"::timestamp::int
[1727341930684550]

select [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector)
[0.481455]
```
