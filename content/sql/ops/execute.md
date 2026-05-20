---
weight: 4
title: "EXECUTE"
bookToc: true
---

# EXECUTE Statement

```SQL
EXECUTE function_name[(value, ...)]
```

Execute a function.

Other ways to execute a function include [SELECT](/docs/sql/ops/query/select)
or using the [JSON-RPC API](/docs/api/http).

---

```SQL
CREATE FUNCTION json_sum(a int, b int) RETURN json
BEGIN
  RETURN {
    "a": a,
    "b": b,
    "sum": a + b
  };
END;

EXECUTE json_sum(2, 2);

json_sum
────────
{
  "a": 2,
  "b": 2,
  "sum": 4
}
```
