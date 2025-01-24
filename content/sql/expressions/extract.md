---
weight: 15
title: EXTRACT
type: docs
bookToc: false
---

## EXTRACT operator

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

**`EXTRACT`** implemented as an alias to the [extract()](/docs/sql/functions/time) function.

---

```SQL
select extract(us from timestamp '2001-01-16 20:38:40.123456');
[123456]

select extract(us from '2001-01-16 20:38:40.123456'::timestamp);
[123456]

select timestamp '2001-01-16 20:38:40.123456'::extract('us');
[123456]

select extract(min from interval '3 days 2 hr 47 min');
[47]

select '3 days 2 hr 47 min'::interval::extract('min');
[47]
```
