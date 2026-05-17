---
weight: 4
title: "JSON"
bookToc: true
---

# JSON Array Functions

### **`json append(array, ...)`**
### **`json push_back(array, ...)`**

Append one or more values to the JSON **`array`**.

```SQL
SELECT [1]::append(2,3);

append
──────
[1, 2, 3]

SELECT [1]::push_back(2,3);

push_back
─────────
[1, 2, 3]
```

---

### **`json push(array, ...)`**

Add one or more values to the begining of the JSON **`array`**.

```SQL
SELECT [3]::push(1,2);

push
────
[1, 2, 3]
```

---

### **`json pop(array)`**

Remove first element from the JSON **`array`**.

```SQL
SELECT [1,2,3]::pop;

pop
───
[2, 3]

SELECT []::pop;

pop
───
[2, 3]
```
---

### **`json pop_back(array)`**

Remove last element from the JSON **`array`**.

```SQL
SELECT [1,2,3]::pop_back;

pop_back
────────
[1, 2]

SELECT []::pop_back;

pop_back
────────
[]
```

---

### **`json put(array, position, value)`**

Place value in the JSON **`array`** at the **`position`**. The position starts from zero.

```SQL
SELECT [1,2,3]::put(1, 'two');

put
───
[1, "two", 3]
```

---

### **`json remove(array, position)`**

Remove element from the JSON **`array`** at the **`position`**. The position starts from zero.

```SQL
SELECT [1,2,3]::remove(1);

remove
──────
[1, 3]
```

---

# JSON Object Functions

### **`json set(obj, path, value)`**

Set the JSON **`obj`** key at the **`path`** to the **`value`**. The **`path`** can be compound.

```SQL
SELECT {}::set("id", 48);

set
───
{
  "id": 48
}

SELECT {}::set("id", 48)::set("data", [1,2,3]);

set
───
{
  "id": 48,
  "data": [1, 2, 3]
}

SELECT {"a": {"b": 123}}::set("a.b", 321);

set
───
{
  "a": {
    "b": 321
  }
}
```

---

### **`json unset(obj, path)`**

Remove key at the **`path`** from the JSON **`obj`**. The **`path`** can be compound.

```SQL
SELECT {"a": {"b": 123}}::unset("a.b");

unset
─────
{
  "a": {}
}
```

---

### **`bool has(obj, path)`**

Return true if the JSON **`obj`** key at the **`path`** exists. The **`path`** can be compound.

```SQL
SELECT {"a": {"b": 123}}::has("a.b");

has
───
true
```
