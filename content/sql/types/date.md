---
weight: 12
title: DATE
type: docs
bookToc: true
---

# DATE

**`DATE`** type represents date according to the [ISO8601](https://en.wikipedia.org/wiki/ISO_8601).
Internally type converted, stored, and operated as a `32-bit` integer representing [Julian Day](https://en.wikipedia.org/wiki/Julian_day).

The supported range is from **`0001-01-01`** to **`9999-12-31`**.

**`CURRENT_DATE`** and [now()](/docs/sql/builtin/time) can be used to get the current date and transaction time.
**`DATE`** prefix before a string can be used to explicitly define date value without convertion.

[Time Functions](/docs/sql/builtin/time) can do basic operations using timestamps, intervals, and dates.

---

```SQL
SELECT current_date;

current_date
────────────
2026-05-17

SELECT date '2025-01-24' as const;

const
─────
2025-01-24

SELECT '2025-01-24'::date;

date
────
2025-01-24

SELECT now();
["2025-01-24 13:49:08.221255+02"]

SELECT now()::date;

date
────
2026-05-17

SELECT current_date::int;

int
───
2461178

SELECT current_date + interval '5 days 5 hours 5 secs' as ts;

ts
──
2026-05-22 08:00:05+03

SELECT {"date": current_date, "id": show().uuid} as json;

json
────
{
  "date": "2026-05-17",
  "id": "b9b6fbf1-85de-9a0b-63e2-3233e03c6803"
}
```

```SQL
CREATE TABLE example (id serial primary key, inserted_at date);
```
