---
weight: 3
title: "Array"
bookToc: false
---

## Array Functions

All array functions are located in the **`public`** schema, which is default.

### length(array)
### size(array)

Return the **`array`** size

``` SQL
select [1,2,3]::size
[3]
```

---

### append(array, ...)
### push_back(array, ...)

Append one or more values to the **`array`**.

```SQL
select [1]::append(2,3)
[1, 2, 3]

select [1]::push_back(2,3)
[1, 2, 3]
```

---

### push(array, ...)

Add one or more values to the begining of the **`array`**.

```SQL
select [3]::push(1,2)
[1, 2, 3]
```

---

### pop(array)

Remove first element from the **`array`**.

```SQL
select [1,2,3]::pop
[2, 3]

select []::pop
[]
```
---

### pop_back(array)

Remove last element from the **`array`**.

```SQL
select [1,2,3]::pop_back
[1, 2]

select []::pop_back
[]
```

---

### put(array, position, value)

Place value in the **`array`** at the **`position`**. The position starts from zero.

```SQL
select [1,2,3]::put(1, 'two')
[1, "two", 3]
```

---

### remove(array, position)

Remove element from the **`array`** at the **`position`**. The position starts from zero.

```SQL
select [1,2,3]::remove(1)
[1, 3]
```

---
