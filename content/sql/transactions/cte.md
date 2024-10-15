---
weight: 3
title: "CTE"
bookToc: false
---

## Common Table Expressions

```SQL
WITH cte_name1 [(args)] AS ( statement ) [, cte_name2 ...]
```

CTE provides a way to define transactions where statements can use previous statements results.

CTE statements and statements without CTE can be used together. Multiple statements are separated
using the **;** symbol or defined using CTE.

If CTE has arguments, it can be used only as a target ([SELECT FROM cte](/docs/sql/query/select)). This assumes that the
result is an array of arrays (rows) and that the arguments are aliases to the array positions.

If CTE has no arguments, it can be used as a target and in expressions ([SELECT cte](/docs/sql/query/select)).

Amelie generates an optimized parallel plan for executing multi-statement transactions and CTE.
It combines multiple node requests together to reduce wait times and speed up the execution of
non-dependable CTE statements.

### RETURNING

```SQL
RETURNING expression
```

All DML statements have a **`RETURNING`** clause, which allows the assignment of CTE value
after its execution.

### INTO

```SQL
INTO cte_name
```

Alternatively, ALL DML and SELECT statements support the **`INTO`** clause, an alternative
way to define CTE without arguments.

---

```SQL
-- with CTE
with deleted_items as (
    delete from collection returning *
) select count(*) from deleted_items
[3]

-- alternative CTE form using INTO
delete from collection returning * into deleted_items;
select count(*) from deleted_items
[3]

-- CTE in expressions
select 1 + 1 into result; select result
[2]
```
