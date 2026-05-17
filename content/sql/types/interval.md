---
weight: 11
title: INTERVAL
type: docs
bookToc: true
---

## INTERVAL

Define a time **`INTERVAL`** with microsecond precision. This type is similar in spirit to the `INTERVAL` type, which PostgreSQL uses.
The type can be used as a column or part of the expression.

**`INTERVAL`** prefix before a string can be used to define interval value explicitly.
Intervals can be added or subtracted and are mainly used together with timestamps.

**`INTERVAL`** understands combinations of the following modificators:

* years
* year
* months
* month
* weeks
* week
* days
* day
* hours
* hour
* hrs
* hr
* minutes
* minute
* mins
* min
* seconds
* second
* secs
* sec
* milliseconds
* millisecond
* ms
* microseconds
* microsecond
* us

[Time Functions](/docs/sql/builtin/time) can do basic operations using timestamps, intervals, and dates.

---

```SQL
SELECT current_timestamp - interval '5 hours' as expr;

expr
────
2026-05-17 12:18:06.521268+03

SELECT '1 hour 5 minutes 6 seconds'::interval;

interval
────────
1 hour 5 minutes 6 seconds

SELECT interval '1 hour 5 minutes 6 seconds' as const;

const
─────
1 hour 5 minutes 6 seconds
```
