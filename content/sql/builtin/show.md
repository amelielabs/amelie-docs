---
weight: 14
title: "Show"
booktoc: true
---

# Show Functions

Following system functions are aliases for corresponding [SHOW](/docs/sql/ops/show) commands.

---

### **`json show()`**
### **`json show(section)`**
### **`json show(section, name)`**
### **`json show(section, verbose)`**
### **`json show(section, name, verbose)`**
### **`json show(section, name, on, verbose)`**

Get a system catalog information about relations or system status.

```sql
select show().uuid as id;

id
──
"b9b6fbf1-85de-9a0b-63e2-3233e03c6803"

select show('config').uuid as id;

id
──
"b9b6fbf1-85de-9a0b-63e2-3233e03c6803"

select show('tables');

show
────
[{
  "user": "amelie",
  "name": "test"
}, {
  "user": "amelie",
  "name": "example"
}]

SELECT * FROM SHOW TABLES;

tables
──────
{
  "user": "amelie",
  "name": "test"
}
{
  "user": "amelie",
  "name": "example"
}

SELECT show('table', 'test', true).partitioning;

partitioning
────────────
{
  "partitions": 6,
  "volumes": [{
    "name": "main",
    "id": "860c1f08-16d3-52cd-9be6-052613f45ad5",
    "pause": false
  }]
}
```
