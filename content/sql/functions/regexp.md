---
weight: 12
title: "Regexp"
bookToc: false
---

## Regular Expressions

All functions are located in the **`public`** schema, which is default.

All string functions work with UTF-8 encoded strings.

---

### **`bool regexp_like(string, pattern)`**

Return true if the **`string`** matches the **`pattern`**.

```SQL
select 'foobarbequebazilbarfbonk'::regexp_like('(b[^b]+)(b[^b]+)');
[true]

select '<a href="../">Up</a>'::regexp_like('<(?<tag>[a-z][a-z0-9]*)[^>]*>');
[true]
```

---

### **`string regexp_substr(string, pattern)`**

Match and return substring from the **`string`** using the **`pattern`**.

```SQL
select 'foobarbequebazilbarfbonk'::regexp_substr('(b[^b]+)(b[^b]+)');
["barbeque"]
```

---

### **`json regexp_match(string, pattern)`**

Return an array of substrings which matches the **`pattern`**.

```SQL
select 'foobarbequebazilbarfbonk'::regexp_match('(b[^b]+)(b[^b]+)');
[["barbeque", "bar", "beque"]]
```

---

### **`string regexp_replace(string, pattern, with)`**

Match and replace substrings from the **`string`** using the **`pattern`**.

```SQL
select 'foobarbequebazilbarfbonk'::regexp_replace('(b[^b]+)(b[^b]+)', '_');
["foo__bonk"]
```
