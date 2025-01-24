---
weight: 2
title: "Type Casting"
bookToc: false
---
 
## Type Casting

All casting functions are located in the **`public`** schema, which is default.

---

### **`string type(arg)`**

Return string description of the **`arg`** type.

```SQL
select "hello"::type;
["string"]

select {"id": 48}::type;
["json"]
```

---

### **`int int(arg)`**

Convert **`arg`** value to **`int`**.

```SQL
select '1234'::int;
[1234]

select "2024-09-26 12:12:10.684550+03"::timestamp::int;
[1727341930684550]
```

---

### **`bool bool(arg)`**

Convert **`arg`** value to **`bool`**.

```SQL
select 1::bool;
[true]

select 0::bool;
[false]
```

---

### **`double double(arg)`**

Convert **`arg`** value to **`double`**.

```SQL
select type(123::double);
["double"]
```

---

### **`string string(arg)`**

Convert **`arg`** value to **`string`**.

```SQL
select 1234::string;
["1234"]

select {"id": 48, "data": [1,2,3]}::string;
["{\"id\": 48, \"data\": [1, 2, 3]}"]
```

---

### **`json json(arg)`**

Convert **`arg`** value to **`json`**.

```SQL
select 123::json;
[123]

select 123::json::type;
["json"]
```

---

### **`json json_import(string)`**

Parse JSON **`string`** to **`json`** type.

```SQL
select '{"id": 48, "data": [1, 2, 3]}'::json_import;
[{
  "id": 48,
  "data": [1, 2, 3]
}]
```

---

### **`interval interval(string)`**

Convert value from **`string`** to **`interval`**.

```SQL
select '1 hour 5 minutes 6 seconds'::interval;
["1 hour 5 minutes 6 seconds"]
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
select timestamp("2024-09-26 12:12:10.684550+03");
["2024-09-26 12:12:10.684550+03"]

select "2024-09-26 12:12:10.684550+03"::timestamp;
["2024-09-26 12:12:10.684550+03"]

select "2024-09-26 12:12:10.684550+03"::timestamp::int;
[1727341930684550]

select 1727341930684550::timestamp;
["2024-09-26 12:12:10.684550+03"]

show timezone;
["Asia/Famagusta"]

select "2024-09-26 12:12:10.684550"::timestamp('Asia/Famagusta');
["2024-09-26 12:12:10.684550+03"]

select "2024-09-26 12:12:10.684550"::timestamp('UTC');
["2024-09-26 15:12:10.684550+03"]

set timezone to 'UTC'
select "2024-09-26 12:12:10.684550"::timestamp('UTC');
["2024-09-26 12:12:10.684550+00"]

select current_date::timestamp;
["2024-09-26 00:00:00+00"]
```
---

### **`date date(timestamp)`**
### **`date date(string)`**
### **`date date(int)`**

Convert from **`timestamp`**, **`string`** or **`int`** to **`date`**.

```SQL
select "2025-01-24"::date;
["2025-01-24"]

select now()::date;
["2025-01-24"]

select current_date::int::date;
["2025-01-24"]
```

---

### **`vector vector(json)`**

Convert from **`json`** array to **`vector`**. Array values must be integers or floats.

```SQL
select [1.0, 2.1, 3]::vector * [1.5, 1.5, 1.5]::vector;
[1.5, 3.15, 4.5]
```
