---
weight: 4
title: "JSON"
bookToc: false
---

## JSON Array Functions

All array functions are located in the **`public`** schema, which is default.

---


### **`json append(array, ...)`**
### **`json push_back(array, ...)`**

Append one or more values to the JSON **`array`**.

```SQL
select [1]::append(2,3)
[1, 2, 3]

select [1]::push_back(2,3)
[1, 2, 3]
```

---

### **`json push(array, ...)`**

Add one or more values to the begining of the JSON **`array`**.

```SQL
select [3]::push(1,2)
[1, 2, 3]
```

---

### **`json pop(array)`**

Remove first element from the JSON **`array`**.

```SQL
select [1,2,3]::pop
[2, 3]

select []::pop
[]
```
---

### **`json pop_back(array)`**

Remove last element from the JSON **`array`**.

```SQL
select [1,2,3]::pop_back
[1, 2]

select []::pop_back
[]
```

---

### **`json put(array, position, value)`**

Place value in the JSON **`array`** at the **`position`**. The position starts from zero.

```SQL
select [1,2,3]::put(1, 'two')
[1, "two", 3]
```

---

### **`json remove(array, position)`**

Remove element from the JSON **`array`** at the **`position`**. The position starts from zero.

```SQL
select [1,2,3]::remove(1)
[1, 3]
```

---

## JSON Object Functions

All object functions are located in the **`public`** schema, which is default.

---

### **`json set(obj, path, value)`**

Set the JSON **`obj`** key at the **`path`** to the **`value`**. The **`path`** can be compound.

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

### **`json unset(obj, path)`**

Remove key at the **`path`** from the JSON **`obj`**. The **`path`** can be compound.

```SQL
select {"a": {"b": 123}}::unset("a.b")
[{
  "a": {}
}]
```

---

### **`json has(obj, path)`**

Return true if the JSON **`obj`** key at the **`path`** exists. The **`path`** can be compound.

```SQL
select {"a": {"b": 123}}::has("a.b")
[true]
```
