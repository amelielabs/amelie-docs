---
weight: 8
title: TEXT
type: docs
bookToc: false
---

## TEXT

**`TEXT`**, **`STRING`** defines a UTF8 encoded string.

Single quotes or double quotes can be used to define a string. Strings can contain escape characters.

Types can be used as a part of the primary or secondary key.

---

```SQL
select "こんにちは";
["こんにちは"]

select 'Hello World!';
["Hello World"]

select {"text": "Hello " || "World!"};
[{
  "text": "Hello World!"
}]
```

```SQL
create table example (id text primary key);
insert into example values ("hello world");
select id from example;
["hello world"]
```
