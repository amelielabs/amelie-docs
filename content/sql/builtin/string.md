---
weight: 3
title: "String"
bookToc: true
---

# String Functions

All string functions work with UTF-8 encoded strings.

---

### **`int length(arg)`**
### **`int size(arg)`**

Return the size of the argument, which can be **`string`**, **`json`** or **`vector`**.

```SQL
SELECT "こんにちは"::length;

length
──────
5

SELECT "hello"::size;

size
────
5
```

---

### **`int octet_length(arg)`**

Return the size of the argument in bytes, which can be **`string`**, **`json`** or **`vector`**.

```SQL
SELECT "こんにちは"::octet_length;

octet_length
────────────
15
```

---

### **`string concat(...)`**

Concatenate strings. **`NULL`** values will be ignored.

```SQL
SELECT "hello"::concat(" world!");

concat
──────
hello world!

SELECT concat("a", "b", null, "c");

concat
──────
abc
```

---

### **`string lower(string)`**

Convert the ASCII characters of **`string`** to the lowercase presentation.

```SQL
SELECT "HELLO"::lower;

lower
─────
hello
```

---

### **`string upper(string)`**

Convert the ASCII characters of **`string`** to the uppercase presentation.

```SQL
SELECT "hello"::upper;

upper
─────
HELLO
```

---

### **`string substr(string, pos)`**
### **`string substr(string, pos, count)`**

Copy substring starting from **`pos`**. The position starts from one.

```SQL
SELECT "hello world"::substr(7);

substr
──────
world

SELECT "hello world"::substr(7, 2);

substr
──────
wo
```

---

### **`int strpos(string, substring)`**

Return **`substring`** position in the **`string`**. Position starts from one.
If the **`substring`** is not found, zero will be returned.

```SQL
SELECT "hello world"::strpos("world");

strpos
──────
7
```

---

### **`string replace(string, from, to)`**

Replace substring in the **`string`**.

```SQL
SELECT "hello world"::replace("hello", "hi");

replace
───────
hi world
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
SELECT "   \t hello world"::ltrim;

ltrim
─────
hello world

SELECT "XxXxYXZxXhello world"::ltrim("XxYZZ");

ltrim
─────
hello world
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
SELECT 'http://google.com' like '%google%' as expr;

expr
────
true

SELECT 'http://google.com'::like('%google%');

like
────
true
```
