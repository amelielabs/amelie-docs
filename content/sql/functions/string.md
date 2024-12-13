---
weight: 3
title: "String"
bookToc: false
---

## String Functions

All string functions are located in the **`public`** schema, which is default.

---

### **`int length(arg)`**
### **`int size(arg)`**

Return the size of the argument, which can be **`STRING`**, **`JSON`** or **`VECTOR`**.

```SQL
select "hello"::size;
[5]
```

---

### **`string concat(...)`**

Concatenate strings. **`NULL`** values will be ignored.

```SQL
select "hello"::concat(" world!");
["hello world!"]

select concat("a", "b", null, "c");
["abc"]
```

---

### **`string lower(string)`**

Convert the **`string`** to the lowercase presentation.

```SQL
select "HELLO"::lower;
["hello"]
```

---

### **`string upper(string)`**

Convert the **`string`** to the uppercase presentation.

```SQL
select "hello"::upper;
["HELLO"]
```

---

### **`string substr(string, pos)`**
### **`string substr(string, pos, count)`**

Copy substring starting from **`pos`**. The position starts from one.

```SQL
select "hello world"::substr(7);
["world"]

select "hello world"::substr(7, 2);
["wo"]
```

---

### **`int strpos(string, substring)`**

Return **`substring`** position in the **`string`**. Position starts from one.
If the **`substring`** is not found, zero will be returned.

```SQL
select "hello world"::strpos("world");
[7]
```

---

### **`string replace(string, from, to)`**

Replace substring in the **`string`**.

```SQL
select "hello world"::replace("hello", "hi");
["hi world"]
```

---

### **`string ltrim(string)`**
### **`string ltrim(string, filter)`**
### **`string rtrim(string)`**
### **`string rtrim(string, filter)`**
### **`string trim(string)`**
### **`string trim(string, filter)`**

Remove characters defined by the **`filter`** string from the left, right, or left and
right parts of the **`string`**. If **`filter`** is not
defined **`" \t\v\n\f"`** characters will be used.

```SQL
select "   \t hello world"::ltrim;
["hello world"]

select "XxXxYXZxXhello world"::ltrim("XxYZZ");
["hello world"]
```

---

### **`bool like(string, pattern)`**

Identical to the [LIKE](/docs/sql/expressions/like) operator.

Returns true if the **`string`** matches the **`pattern`**.

The **`pattern`** is a regular string with two special characters used for templating:

* **`_`** match any single character
* **`%`** match zero, one or multiple characters

Escape characters can be used to match template characters.

```SQL
select 'http://google.com' like '%google%';
[true]

select 'http://google.com'::like('%google%');
[true]
```
