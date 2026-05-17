---
weight: 10
title: TIMESTAMP
type: docs
bookToc: true
---

## TIMESTAMP

**`TIMESTAMP`** type represents timestamp with a timezone according to the [ISO8601](https://en.wikipedia.org/wiki/ISO_8601)
with microsecond precision. This type is similar to `TIMESTAMPTZ` used by PostgreSQL.
The type can be used as a column type or a key.

Internally type converted, stored, and operated as a `64-bit` integer representing Unix time in UTC.
All operations are corrected according to the current timezone settings.

The supported range is from **`1970-01-01 00:00:00.000000`** to **`9999-12-31 23:59:59.999999`**.

**`CURRENT_TIMESTAMP`** and [now()](/docs/sql/builtin/time) can be used to get the current transaction time.
**`TIMESTAMP`** prefix before a string can be used to explicitly define timestamp value without convertion.

[Time Functions](/docs/sql/builtin/time) can do basic operations using timestamps, intervals, and dates.

---

```SQL
SELECT now(), current_timestamp;

now                               current_timestamp
────────────────────────────────────────────────────────────────────
2026-05-17 17:11:26.953909+03     2026-05-17 17:11:26.953909+03

SELECT show().timezone;

timezone
────────
"Asia/Famagusta"

SELECT current_timestamp - interval '5 hours' as expr;

expr
────
2026-05-17 12:12:41.498522+03

SELECT timestamp "2024-09-26 12:12:10.684550+03" as const;

const
─────
2024-09-26 12:12:10.684550+03

SELECT "2024-09-26 12:12:10.684550+03"::timestamp;

timestamp
─────────
2024-09-26 12:12:10.684550+03

SELECT "2024-09-26 12:12:10.684550+03"::timestamp::int;

int
───
1727341930684550

SELECT 1727341930684550::timestamp;

timestamp
─────────
2024-09-26 12:12:10.684550+03

SELECT {
  "at": now(),
  "id": show('config').uuid
} as json;

json
────
{
  "at": "2026-05-17 17:16:05.048230+03",
  "id": "b9b6fbf1-85de-9a0b-63e2-3233e03c6803"
}
```

```SQL
CREATE TABLE example (ts timestamp primary key, metrics json);
```
