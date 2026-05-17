---
weight: 12
title: "Regexp"
bookToc: true
---

# Regular Expressions

All string functions work with UTF-8 encoded strings.

---

### **`bool regexp_like(string, pattern)`**

Return true if the **`string`** matches the **`pattern`**.

```SQL
SELECT 'foobarbequebazilbarfbonk'::regexp_like('(b[^b]+)(b[^b]+)');

regexp_like
───────────
true

SELECT '<a href="../">Up</a>'::regexp_like('<(?<tag>[a-z][a-z0-9]*)[^>]*>');

regexp_like
───────────
true
```

---

### **`string regexp_substr(string, pattern)`**

Match and return substring from the **`string`** using the **`pattern`**.

```SQL
SELECT 'foobarbequebazilbarfbonk'::regexp_substr('(b[^b]+)(b[^b]+)');

regexp_substr
─────────────
barbeque
```

---

### **`json regexp_match(string, pattern)`**

Return an array of substrings which matches the **`pattern`**.

```SQL
SELECT 'foobarbequebazilbarfbonk'::regexp_match('(b[^b]+)(b[^b]+)');

regexp_match
────────────
["barbeque", "bar", "beque"]
```

---

### **`string regexp_replace(string, pattern, with)`**

Match and replace substrings from the **`string`** using the **`pattern`**.

```SQL
SELECT 'foobarbequebazilbarfbonk'::regexp_replace('(b[^b]+)(b[^b]+)', '_');

regexp_replace
──────────────
foo__bonk
```
