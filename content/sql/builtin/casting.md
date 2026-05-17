---
weight: 2
title: "Casting"
bookToc: true
---
 
# Type Casting

### **`string type(arg)`**

Return string description of the **`arg`** type.

```SQL
SELECT "hello"::type;

type
────
string

SELECT {"id": 48}::type;

type
────
json
```

---

### **`int int(arg)`**

Convert **`arg`** value to **`int`**.

```SQL
SELECT '1234'::int;

int
───
1234

SELECT "2024-09-26 12:12:10.684550+03"::timestamp::int;

int
───
1727341930684550
```

---

### **`bool bool(arg)`**

Convert **`arg`** value to **`bool`**.

```SQL
SELECT 1::bool;

bool
────
true

SELECT 0::bool;

bool
────
false
```

---

### **`double double(arg)`**

Convert **`arg`** value to **`double`**.

```SQL
SELECT type(123::double);

type
────
double
```

---

### **`string string(arg)`**

Convert **`arg`** value to **`string`**.

```SQL
SELECT 1234::string;

string
──────
1234

SELECT {"id": 48, "data": [1,2,3]}::string;

string
──────
{"id": 48, "data": [1, 2, 3]}
```

---

### **`json json(arg)`**

Convert **`arg`** value to **`json`**.

```SQL
SELECT 123::json;

json
────
123

SELECT 123::json::type;

type
────
json
```

---

### **`json json_import(string)`**

Parse JSON **`string`** to **`json`** type.

```SQL
SELECT '{"id": 48, "data": [1, 2, 3]}'::json_import;

json_import
───────────
{
  "id": 48,
  "data": [1, 2, 3]
}
```

---

### **`interval interval(string)`**

Convert value from **`string`** to **`interval`**.

```SQL
SELECT '1 hour 5 minutes 6 seconds'::interval;

interval
────────
1 hour 5 minutes 6 seconds
```

---

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

select "2024-09-26 12:12:10.684550+03"::timestamp;

timestamp
─────────
2024-09-26 12:12:10.684550+03

select "2024-09-26 12:12:10.684550+03"::timestamp::int;

int
───
1727341930684550

select 1727341930684550::timestamp;

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

### **`date date(timestamp)`**
### **`date date(string)`**
### **`date date(int)`**

Convert from **`timestamp`**, **`string`** or **`int`** to **`date`**.

```SQL
SELECT "2025-01-24"::date;

date
────
2025-01-24

SELECT now()::date;

date
────
2026-05-17

SELECT current_date::int::date;

date
────
2026-05-17
```

---

### **`vector vector(json)`**

Convert from **`json`** array to **`vector`**. Array values must be integers or floats.

```SQL
SELECT [1.0, 2.1, 3]::vector;

vector
──────
[1, 2.1, 3]
```

---

### **`uuid uuid(string)`**

Convert from **`string`** to **`uuid`**.

```SQL
SELECT "4845888e-dbc4-88bc-2e22-9673ccd23bee"::uuid;

uuid
────
4845888e-dbc4-88bc-2e22-9673ccd23bee
```
