---
weight: 12
title: CASE
type: docs
bookToc: false
---

## CASE operator

```SQL
CASE [expr] [WHEN expr THEN expr]
            ...
            [ELSE expr]
END
```

**`CASE`** construct implements a basic condition operator. It has two forms:

* **`CASE with expression`**

  `CASE` returns the result of the **`THEN`** clause if the result of its expression matches the result of the first **`WHEN`** clause.

* **`CASE without expression`**

  `CASE` returns the result of the **`THEN`** clause if its corresponding **`WHEN`** clause evaluates to true.

For both cases, if no matches are found, the result of the **`ELSE`** clause will be returned or **`NULL`**
if the **`ELSE`** clause is not defined. All expression types must match.

---

```SQL
-- case expr with else
select
	case 0
		when 1 then 1
		when 2 then 2
		else 3
	end;
[3]

-- case expr
select
	case 0
		when 1 then 1
		when 2 then 2
	end;
[null]

-- case without expr
select
	case
		when id = 2 then 'found'
		else 'not found'
	end
from test;
["not found", "found", "not found"]
```
