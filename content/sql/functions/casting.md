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
select "hello"::type
["string"]

select {"id": 48}::type
["json"]
```

---

### **`int int(arg)`**

Convert **`arg`** value to **`INT`**.

```SQL
select '1234'::int
[1234]

select "2024-09-26 12:12:10.684550+03"::timestamp::int
[1727341930684550]
```

---

### **`bool bool(arg)`**

Convert **`arg`** value to **`BOOL`**.

```SQL
select 1::bool
[true]

select 0::bool
[false]
```

---

### **`double double(arg)`**

Convert **`arg`** value to **`DOUBLE`**.

```SQL
select type(123::double)
["double"]
```

---

### **`string string(arg)`**

Convert **`arg`** value to **`STRING`**.

```SQL
select 1234::string
["1234"]

select {"id": 48, "data": [1,2,3]}::string
["{\"id\": 48, \"data\": [1, 2, 3]}"]
```

---

### **`json json(arg)`**

Convert **`arg`** value to **`JSON`**.

```SQL
select 123::json
[123]

select 123::json::type
["json"]
```

---

### **`json json_import(string)`**

Parse JSON **`STRING`** to **`JSON`** type.

```SQL
select '{"id": 48, "data": [1, 2, 3]}'::json_import
[{
  "id": 48,
  "data": [1, 2, 3]
}]
```

---

### **`interval interval(string)`**

Convert value from **`STRING`** to **`INTERVAL`**.

```SQL
select '1 hour 5 minutes 6 seconds'::interval
["1 hour 5 minutes 6 seconds"]
```

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

### **`vector vector(json)`**

Convert from **`JSON`** array to **`VECTOR`**. Array values must be integers or floats.

```SQL
select [1.0, 2.1, 3]::vector * [1.5, 1.5, 1.5]::vector
[1.5, 3.15, 4.5]
```
