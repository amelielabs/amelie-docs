---
weight: 4
title: TEXT
type: docs
bookToc: false
---

## TEXT

Defines a UTF8 encoded string. The types **`TEXT`** and **`STRING`** are synonymous.

Single quotes or double quotes can be used to define a string. Strings can contain escape characters.

Types can be used as a part of the primary or secondary key.

---

```SQL
select "Hello World!"
["Hello World"]

select 'Hello World!'
["Hello World"]

select {"text": "Hello " || "World!"}
[{
  "text": "Hello World!"
}]
```

```SQL
create table example(id text primary key)
```
