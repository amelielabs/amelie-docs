---
weight: 2
title: "BEGIN/COMMIT"
bookToc: false
---

## BEGIN / COMMIT Statements

```SQL
[BEGIN]
statement[; statement ...]
[COMMIT]
```

Amelie transactions are not non-interactive and require that all transaction statements must
be provided for execution.

Multiple statements are separated using the **;** symbol or defined using CTE.

**`BEGIN/COMMIT`** statements are optional and can mostly be used to parse multi-statement
transactions. If **`BEGIN`** is defined, it must be strictly at the
beginning of the transaction, followed by the **`COMMIT`** statement at the end.

All provided statements are always atomical and transactional, regardless of whether
there were **`BEGIN/COMMIT`** statements.

---

```SQL
begin
update accounts set ammount = ammount + 5 where client = 1;
update accounts set ammount = ammount - 5 where client = 2;
commit
```
