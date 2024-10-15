---
weight: 4
title: "Object"
bookToc: false
---

## Object Functions

All object functions are located in the **`public`** schema, which is default.

### length(obj)
### size(obj)

Return the **`obj`** size.

``` SQL
select {"a": 1, "b": 2, "c": 3}::size
[3]
```

---

### set(obj, path, value)

Set the **`obj`** key at the **`path`** to the **`value`**. The **`path`** can be compound.

```SQL
select {}::set("id", 48)
[{
  "id": 48
}]

select {}::set("id", 48)::set("data", [1,2,3])
[{
  "id": 48,
  "data": [1, 2, 3]
}]

select {"a": {"b": 123}}::set("a.b", 321)
[{
  "a": {
    "b": 321
  }
}]
```

---

### unset(obj, path)

Remove key at the **`path`** from the **`obj`**. The **`path`** can be compound.

```SQL
select {"a": {"b": 123}}::unset("a.b")
[{
  "a": {}
}]
```

---

### has(obj, path)

Return true if the **`obj`** key at the **`path`** exists. The **`path`** can be compound.

```SQL
select {"a": {"b": 123}}::has("a.b")
[true]
```
