---
weight: 6
title: "Timestamp"
bookToc: false
---

## Timestamp Function

All timestamp functions are located in the **`public`** schema, which is default.

### timestamp(string)
### timestamp(string, timezone)
### timestamp(int)

Convert from **`STRING`** to **`TIMEZONE`**. If the **`timezone`** argument is provided, the
timestamp will be created according to it.

Convert from **`INT`** to **`TIMEZONE`**. The first argument is expected to be the
Unix epoch in UTC with microsecond precision.

```SQL
select timestamp("2024-09-26 12:12:10.684550+03")
["2024-09-26 12:12:10.684550+03"]

select "2024-09-26 12:12:10.684550+03"::timestamp
["2024-09-26 12:12:10.684550+03"]

select "2024-09-26 12:12:10.684550+03"::timestamp::int
[1727341930684550]

select 1727341930684550::timestamp
["2024-09-26 12:12:10.684550+03"]

show timezone
["Asia/Famagusta"]

select "2024-09-26 12:12:10.684550"::timestamp('Asia/Famagusta')
["2024-09-26 12:12:10.684550+03"]

select "2024-09-26 12:12:10.684550"::timestamp('UTC')
["2024-09-26 15:12:10.684550+03"]

set timezone to 'UTC'
select "2024-09-26 12:12:10.684550"::timestamp('UTC')
["2024-09-26 12:12:10.684550+00"]
```

---

### now()

Get transaction time.

```SQL
select now()
["2024-09-28 17:40:08.876414+03"]
```

---

### at_timezone(timestamp, timezone)

Do explicit convertion of **`timestamp`** to the **`timezone`**,
function returns **`string`**.

```SQL
show timezone
["asia/famagusta"]

select now(), now()::at_timezone('Japan')
["2024-09-28 17:43:12.403002+03", "2024-09-28 23:43:12.403002+09"]
```

---

### generate_series(start timestamp, end timestamp, step interval)

Create and return an array of timestamp values between **`start`** and **`end`**
with the **`step`** interval. The **`end`** timestamp is inclusive.

Please note that this function is not intended for large ranges since it
allocates result in memory.

```SQL
select now()
["2024-09-28 17:52:37.449741+03"]

select * from generate_series(now() - interval '1 hour', now(), interval '5 min')
["2024-09-28 16:51:33.549038+03", "2024-09-28 16:56:33.549038+03", "2024-09-28 17:01:33.549038+03",
 "2024-09-28 17:06:33.549038+03", "2024-09-28 17:11:33.549038+03", "2024-09-28 17:16:33.549038+03",
 "2024-09-28 17:21:33.549038+03", "2024-09-28 17:26:33.549038+03", "2024-09-28 17:31:33.549038+03",
 "2024-09-28 17:36:33.549038+03", "2024-09-28 17:41:33.549038+03", "2024-09-28 17:46:33.549038+03",
 "2024-09-28 17:51:33.549038+03"]
```

---

### date_bin(interval, timestamp)
### date_bin(interval, timestamp, timestamp_origin)
### date_bin(timestamp, interval)
### date_bin(timestamp, interval, timestamp_origin)

Align the **`timestamp`** with the **`interval`** using the origin timestamp. If the
origin timestamp is not provided, it will be set as **`2001-01-01 00:00:00`**.

```SQL
select now(), date_bin(interval '15 minutes', now())
["2024-09-28 18:06:05.698093+03", "2024-09-28 18:00:00+03"

select now(), now()::date_bin(interval '15 minutes')
["2024-09-28 18:06:53.966574+03", "2024-09-28 18:00:00+03"]

select now()
["2024-09-29 10:56:52.753882+03"]

select *, count(*)
from generate_series(now() - interval '1 hour', now() - interval '1 min', interval '1 min')
group by date_bin(interval '15 minutes', *, now() - interval '1 hour')
order by *;
[["2024-09-29 09:56:53.681898+03", 15], ["2024-09-29 10:11:53.681898+03", 15],
 ["2024-09-29 10:26:53.681898+03", 15], ["2024-09-29 10:41:53.681898+03", 15]]
```

---

### date_trunc(string, interval)
### date_trunc(interval, string)
### date_trunc(string, timestamp)
### date_trunc(string, timestamp, timezone)
### date_trunc(timestamp, string)
### date_trunc(timestamp, string, timezone)

Truncate **`interval`** or **`timestamp`** to the specified precision field.

Supported precisions are:

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

```SQL
select date_trunc(INTERVAL '3 days 2 hr 47 min 33 sec', 'hour')
["3 days 2 hours"]

select '3 days 2 hr 47 min 33 sec'::interval::date_trunc('hour')
["3 days 2 hours"]

select '2001-02-16 20:38:40.123456+00'::timestamp::date_trunc('hour')
["2001-02-16 20:00:00+00"]
```

---

### extract(string, interval)
### extract(interval, string)
### extract(string, timestamp)
### extract(string, timestamp, timezone)
### extract(timestamp, string)
### extract(timestamp, string, timezone)

Extract the time-specific value from the **`timestamp`** or **`interval`**.

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


```SQL
select extract(us from '2001-01-16 20:38:40.123456'::timestamp)
[123456]

select timestamp '2001-01-16 20:38:40.123456'::extract('us')
[123456]

select extract(min from interval '3 days 2 hr 47 min')
[47]

select '3 days 2 hr 47 min'::interval::extract('min')
[47]
```
