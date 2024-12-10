---
weight: 8
title: TEXT
type: docs
bookToc: false
---

## TEXT

Defines a UTF8 encoded string. Types can be used as a part of the primary or secondary key.

* **`TEXT`**, **`STRING`**

	Single quotes or double quotes can be used to define a string. Strings can contain escape characters.

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
create table test(id text primary key)
insert into test values ("hello world")
select id from test
["Hello World"]
```
