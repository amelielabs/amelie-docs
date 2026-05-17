---
weight: 6
title: "Time"
bookToc: true
---

# Time Functions

### **`timestamp timestamp(string, timezone)`**
### **`timestamp timestamp(string)`**
### **`timestamp timestamp(int)`**
### **`timestamp timestamp(date)`**

Convert from **`string`** to **`timestamp`**. If the **`timezone`** argument is provided, the
timestamp will be created according to it.

Convert from **`int`** to **`timestamp`**. The first argument is expected to be the
Unix epoch in UTC with microsecond precision.

Convert from **`date`** to **`timestamp`**. The time will be set to **`00:00:00`**.

```SQL
SELECT timestamp("2024-09-26 12:12:10.684550+03");

timestamp
─────────
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

SHOW timezone;

timezone
────────
"Asia/Famagusta"

SELECT "2024-09-26 12:12:10.684550"::timestamp('Asia/Famagusta');

timestamp
─────────
2024-09-26 12:12:10.684550+03

SELECT "2024-09-26 12:12:10.684550"::timestamp('UTC');

timestamp
─────────
2024-09-26 15:12:10.684550+03
```

---

### **`timestamp now()`**

Get transaction time.

```SQL
SELECT now();

now
───
2026-05-17 19:07:11.549954+03

SELECT current_timestamp;

current_timestamp
─────────────────
2026-05-17 19:07:11.549954+03
```

---

### **`string at_timezone(timestamp, timezone)`**

Do explicit convertion of **`timestamp`** to the **`timezone`**,
function returns **`string`**.

```SQL
SHOW timezone;

timezone
────────
"Asia/Famagusta"

SELECT now(), now()::at_timezone('Japan');

now                               at_timezone
─────────────────────────────────────────────────────────────────
2026-05-17 19:08:11.002193+03     2026-05-18 01:08:11.002193+09
```

---

### **`timestamp date_bin(interval, timestamp)`**
### **`timestamp date_bin(interval, timestamp, timestamp_origin)`**
### **`timestamp date_bin(timestamp, interval)`**
### **`timestamp date_bin(timestamp, interval, timestamp_origin)`**

Align the **`timestamp`** with the **`interval`** using the origin timestamp. If the
origin timestamp is not provided, it will be set as **`2001-01-01 00:00:00`**.

```SQL
SELECT now(), date_bin(interval '15 minutes', now());

now                               date_bin
────────────────────────────────────────────────────────────────────
2026-05-17 19:10:01.142653+03     2026-05-17 19:00:00+03

SELECT now(), current_timestamp::date_bin(interval '15 minutes');

now                               date_bin
────────────────────────────────────────────────────────────────────
2026-05-17 19:10:01.142653+03     2026-05-17 19:00:00+03
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
SELECT '2001-02-16 20:38:40.123456+00'::timestamp::date_trunc('hour');

date_trunc
──────────
2001-02-16 20:00:00+02
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
SELECT interval_trunc(INTERVAL '3 days 2 hr 47 min 33 sec', 'hour');

interval_trunc
──────────────
3 days 2 hours

SELECT '3 days 2 hr 47 min 33 sec'::interval::interval_trunc('hour');

interval_trunc
──────────────
3 days 2 hours
```

---

### **`int extract(string, interval)`**
### **`int extract(string, timestamp)`**
### **`int extract(string, timestamp, timezone)`**
### **`int extract(string, date)`**
### **`int extract(interval, string)`**
### **`int extract(timestamp, string)`**
### **`int extract(timestamp, string, timezone)`**
### **`int extract(date, string)`**

Extract the time-specific value from the **`timestamp`**, **`interval`** or **`date`**.

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
SELECT extract(us from '2001-01-16 20:38:40.123456'::timestamp);

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
