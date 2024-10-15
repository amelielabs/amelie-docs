---
weight: 4
title: "Lambda"
bookToc: false
---

## Lambda

```SQL
SELECT lambda name (expr) = expr
```

Amelie allows lambda expressions.

Lambda is a unique construct that combines the functionality of a function and an
aggregate function with a state.

Lambda is determined by name and two expressions. The first is the initial expression,
which is executed upon creation and determines its type. The second expression is
executed on each iteration and continuously updates its value.

Lambda expressions can help work with arrays and objects and do some non-trivial transformations.

Lambda can be used with shared tables and expressions, but it currently cannot be
used with distributed tables (currently lambda does not support partial state merging).

---

```SQL
select lambda total(0) = total + 1 from [1,2,3]
[3]

select lambda total(0) = total + 1 from [1,2,2,3] group by *
[1, 2, 1]

select lambda first_agg(null) = first_agg::coalesce(*) from [1,2,3]
[1]

select lambda last_agg(null) = * from [1, 2, null]
[2]

select lambda str_agg("") = str_agg::concat(*::string) from [1,2,3]
["123"]

select lambda array_agg([]) = array_agg::append(*) from [1,2,3]
[[1, 2, 3]]

select lambda obj_agg({}) = obj_agg::set("key" || *::string, *) from [1,2,3]
[{
  "key1": 1,
  "key2": 2,
  "key3": 3
}]

select {
  "sums": lambda md5_agg([]) = md5_agg::append(*::string::md5)
} from [1,2,3];
[{
  "sums": ["c4ca4238a0b923820dcc509a6f75849b", "c81e728d9d4c2f636f067f89cc14862c",
           "eccbc87e4b5ce2fe28308fd9f2a7baf3"]
}]
```

```SQL
create shared table test (id int primary key)
insert into test values (1), (2), (3)

select lambda total(0) = total + 1 from test
[3]

select lambda array_agg([]) = array_agg::append(id) from test
[[1, 2, 3]]

select lambda reverse_agg([]) = reverse_agg::push(id) from test
[[3, 2, 1]]

select (lambda reverse_agg([]) = reverse_agg::push(id))::string from test
["[3, 2, 1]"]
```
