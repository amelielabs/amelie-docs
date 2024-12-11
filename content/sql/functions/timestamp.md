---
weight: 6
title: "Timestamp"
bookToc: false
---

## Timestamp Functions

All timestamp functions are located in the **`public`** schema, which is default.

---

### **`timestamp timestamp(string, timezone)`**
### **`timestamp timestamp(string)`**
### **`timestamp timestamp(int)`**

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

### **`timestamp now()`**

Get transaction time.

```SQL
select now()
["2024-09-28 17:40:08.876414+03"]
```

---

### **`string at_timezone(timestamp, timezone)`**

Do explicit convertion of **`timestamp`** to the **`timezone`**,
function returns **`string`**.

```SQL
show timezone
["asia/famagusta"]

select now(), now()::at_timezone('Japan')
["2024-09-28 17:43:12.403002+03", "2024-09-28 23:43:12.403002+09"]
```

---

### **`timestamp date_bin(interval, timestamp)`**
### **`timestamp date_bin(interval, timestamp, timestamp_origin)`**
### **`timestamp date_bin(timestamp, interval)`**
### **`timestamp date_bin(timestamp, interval, timestamp_origin)`**

Align the **`timestamp`** with the **`interval`** using the origin timestamp. If the
origin timestamp is not provided, it will be set as **`2001-01-01 00:00:00`**.

```SQL
select now(), date_bin(interval '15 minutes', now())
["2024-09-28 18:06:05.698093+03", "2024-09-28 18:00:00+03"

select now(), now()::date_bin(interval '15 minutes')
["2024-09-28 18:06:53.966574+03", "2024-09-28 18:00:00+03"]

select now()
["2024-09-29 10:56:52.753882+03"]
```

---

### **`timestamp date_trunc(string, timestamp)`**
### **`timestamp date_trunc(string, timestamp, timezone)`**
### **`timestamp date_trunc(timestamp, string)`**
### **`timestamp date_trunc(timestamp, string, timezone)`**

Truncate **`timestamp`** to the specified precision field.

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
select '2001-02-16 20:38:40.123456+00'::timestamp::date_trunc('hour')
["2001-02-16 20:00:00+00"]
```

---

### **`interval interval_trunc(string, interval)`**
### **`interval interval_trunc(interval, string)`**

Truncate **`interval`** specified precision field.

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
select interval_trunc(INTERVAL '3 days 2 hr 47 min 33 sec', 'hour')
["3 days 2 hours"]

select '3 days 2 hr 47 min 33 sec'::interval::interval_trunc('hour')
["3 days 2 hours"]
```

---

### **`int extract(string, interval)`**
### **`int extract(interval, string)`**
### **`int extract(string, timestamp)`**
### **`int extract(string, timestamp, timezone)`**
### **`int extract(timestamp, string)`**
### **`int extract(timestamp, string, timezone)`**

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
