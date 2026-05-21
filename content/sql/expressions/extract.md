---
weight: 15
title: EXTRACT
type: docs
bookToc: true
---

# EXTRACT operator

```SQL
EXTRACT(field FROM expr)
```

The **`EXTRACT`** operator extracts the time-specific value **`field`** from the
**`expression`**. Supported expression types are **`TIMESTAMP`**, **`INTERVAL`** and **`DATE`**.

Supported fields are:

* year
* month
* day
* hour
* hr
* minute
* min
* sec
* second
* millisecond
* ms
* microsecond
* us

**`EXTRACT`** implemented as an alias to the [extract()](/docs/sql/builtin/time) function.

---

```SQL
SELECT extract(us from timestamp '2001-01-16 20:38:40.123456');

extract
───────
123456

SELECT timestamp '2001-01-16 20:38:40.123456'::extract('us');

extract
───────
123456

SELECT extract(min from interval '3 days 2 hr 47 min');

extract
───────
47

SELECT '3 days 2 hr 47 min'::interval::extract('min');

extract
───────
47
```
