---
weight: 11
title: INTERVAL
type: docs
bookToc: false
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

---

```SQL
select current_timestamp - interval '5 hours';
["2024-09-26 12:12:10.684550+03"]

select '1 hour 5 minutes 6 seconds'::interval;
["1 hour 5 minutes 6 seconds"]

select interval '1 hour 5 minutes 6 seconds';
["1 hour 5 minutes 6 seconds"]
```
