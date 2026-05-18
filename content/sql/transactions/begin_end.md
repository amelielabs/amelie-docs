---
weight: 12
title: "BEGIN / END"
bookToc: true
---

# BEGIN / END Statements

```SQL
[EXPLAIN | PROFILE]
[BEGIN]
statement[; statement ...]
[END]
```

Amelie supports multi-statement ACID transactions and
require that all transaction statements are known and provided for execution together.

It is not intended for long, complex, multi-statement transactions or queries that generate large amounts of data.
There are [configurable limits](/docs/db/admin/configuration) for transaction sizes.

All transactions always operate on a **`STRICT SERIALIZABLE`** level.

To define a multi-statement transaction, the **`BEGIN`** statement be used. it must be strictly at
the beginning of the transaction, followed by the **`END`** statement at the end.

Multiple statements are separated using the **;** symbol or defined using CTE.

Currently **`DDL`** commands cannot be part of a multi-statement transactions.

Amelie does not support dedicated **`COMMIT`** statement.

[EXPLAIN/PROFILE](/docs/sql/ops/query/explain) commands can be used to get more details about the transaction.

---

```SQL
BEGIN;
UPDATE accounts SET ammount = ammount + 5 WHERE client = 1;
UPDATE accounts SET ammount = ammount - 5 WHERE client = 2;
END;
```
