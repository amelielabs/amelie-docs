---
weight: 16
title: CAST
type: docs
bookToc: false
---

## CAST operator

```SQL
CAST (expr AS type)
```

**`CAST`** operator is used to convert the **`expression`** from one type to another.

**`CAST`** implemented as an alias to the [casting](/docs/sql/functions/casting) functions.

---

```SQL
select cast('1234' as int);
[1234]

select cast("2024-09-26 12:12:10.684550+03" as timestamp);
["2024-09-26 12:12:10.684550+03"]

select cast({"data": [1,2,3]} as string);
["{\"data\": [1, 2, 3]}"]
```
