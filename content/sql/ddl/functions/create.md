---
weight: 1
title: "CREATE FUNCTION"
bookToc: true
---

# CREATE FUNCTION

```SQL
CREATE [OR REPLACE] FUNCTION name ([args])
[RETURN type]
BEGIN
  [DECLARE variable_name type] | [STATEMENT]
  ...
END
```

Create a new User-defined Function (UDF) or replace it if it exists.

The current user or agent becomes the owner of the function.

Functions allow you to organize database interactions in a structured and controlled way.
They are stored in compiled form, providing a faster, more secure way to work with the database.

Functions can be used in [SELECT](/docs/sql/ops/query/select) expressions or called using the [EXECUTE](/docs/sql/ops/execute)
command or [HTTP/JSON-RPC API](/docs/api/http).

Functions are strictly typed. The **REPLACE** requires that the new function have
the same return type and arguments.

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

SELECT json_sum(2, 2);

json_sum
────────
{
  "a": 2,
  "b": 2,
  "sum": 4
}
```

```SQL
CREATE FUNCTION reverse(list json) RETURN json
BEGIN
  DECLARE rev json;
  SELECT [] -> self::push(it) INTO rev FROM (list) it;
  RETURN rev;
END;

SELECT [1,2,3]::reverse;

reverse
───────
[3, 2, 1]

SELECT [1,2,3]::reverse::reverse;

reverse
───────
[1, 2, 3]
```
