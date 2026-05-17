---
weight: 12
title: "BEGIN / COMMIT"
bookToc: true
---

## BEGIN / COMMIT Statements

```SQL
[EXPLAIN | PROFILE]
[BEGIN]
statement[; statement ...]
[COMMIT]
```

Amelie transactions require that all transaction statements must be provided for execution.

If **`BEGIN`** is defined, it must be strictly at the beginning of the transaction,
followed by the **`COMMIT`** statement at the end.
Multiple statements are separated using the **;** symbol or defined using CTE.

All provided statements are always atomical and transactional, regardless of whether
there were **`BEGIN/COMMIT`** statements.

---

```SQL
BEGIN;
UPDATE accounts SET ammount = ammount + 5 WHERE client = 1;
UPDATE accounts SET ammount = ammount - 5 WHERE client = 2;
END;
```
