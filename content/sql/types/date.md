---
weight: 12
title: DATE
type: docs
bookToc: false
---

## DATE

**`DATE`** type represents date according to the [ISO8601](https://en.wikipedia.org/wiki/ISO_8601).
Internally type converted, stored, and operated as a 32-bit integer representing [Julian Day](https://en.wikipedia.org/wiki/Julian_day).

The supported range is from **`0001-01-01`** to **`9999-12-31`**.

**`CURRENT_DATE`** and [now()](/docs/sql/functions/time) can be used to get the current date and transaction time.
**`DATE`** prefix before a string can be used to explicitly define date value without convertion.

[Time Functions](/docs/sql/functions/time) can do basic operations using timestamps, intervals, and dates.

---

```SQL
select current_date;
["2025-01-24"]

select date "2025-01-24";
["2025-01-24"]

select "2025-01-24"::date;
["2025-01-24"]

select now();
["2025-01-24 13:49:08.221255+02"]

select now()::date;
["2025-01-24"]

select current_date::int;
[2460700]

select current_date + interval '5 days 5 hours 5 secs';
["2025-01-29 05:00:05+00"]

select {"date": current_date, "id": system.config().uuid};
[{
  "date": "2025-01-24",
  "id": "c86e5e6b-caba-0f78-4c2e-7cb13f5a588a"
}]
```

```SQL
create table example (id serial primary key, inserted_at date);
insert into example (inserted_at) values (current_date);
select * from example
[[0, "2025-01-24"]]
```
