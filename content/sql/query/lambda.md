---
weight: 4
title: "Lambda"
bookToc: false
---

## Lambda

```SQL
SELECT expr -> expr
```

Lambda is a unique construct that combines the functionality of a function and an
aggregate function with a state.

Lambda is defined by using the **`->`** arrow operator.

Each lambda has two expressions. The first is the initial expression,
which is executed upon creation and determines its type and the initial state.
It is executed outside of the iteration scope, which means it cannot access target columns
at this stage. The second expression is executed on each iteration and continuously
updates its state. Both expression types must match.

The special keyword **`self`** can be used inside the right expression to get the current
lambda state.

Lambda expressions can help work with JSON and do some non-trivial transformations.

Lambda can be used with single partition tables and expressions.

---

```SQL
create table example (id int primary key) partitions 1;
insert into example values (1), (2), (3);

-- similair to count(*)
select 0 -> self + 1 from example;
[3]

-- aggregate into string
select "" -> self::concat(id::string) from example;
["123"]

-- aggregate into JSON array
select [] -> self::append(id) from example;
[[1, 2, 3]]

-- aggregate into JSON array in reverse
select [] -> self::push(id) from example;
[[3, 2, 1]]

-- aggregate into JSON object
select {} -> self::set("key_" || id::string, id) from example;
[{
  "key_1": 1,
  "key_2": 2,
  "key_3": 3
}]

-- aggregate average using two lambdas
select (0.0 -> self + id) / (0 -> self + 1) from example;
[2]

-- build json object with field which contains aggregated md5 sums
select {"hashes": [] -> self::append(id::string::md5)} from example;
[{
  "hashes": ["c4ca4238a0b923820dcc509a6f75849b", "c81e728d9d4c2f636f067f89cc14862c",
             "eccbc87e4b5ce2fe28308fd9f2a7baf3"]
}]

-- aggregate with GROUP BY
select id, 0 -> self + 1 from example group by id;
[[1, 1], [2, 1], [3, 1]]
```
