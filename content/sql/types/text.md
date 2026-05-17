---
weight: 8
title: TEXT
type: docs
bookToc: true
---

## TEXT

**`TEXT`**, **`STRING`** defines a UTF8 encoded string.

Single quotes or double quotes can be used to define a string. Strings can contain escape characters.

Types can be used as a part of the primary or secondary key.

---

```SQL
SELECT 'こんにちは' as example;

example
───────
こんにちは

SELECT 'Hello World!' as example;

example
───────
Hello World!
```

```SQL
CREATE TABLE example (id text primary key);
```
