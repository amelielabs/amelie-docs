---
weight: 7
title: "Vector"
bookToc: true
---

# Vector Functions

### **`vector vector(json)`**

Convert from **`json`** array to **`vector`**. Array values must be integers or floats.

```SQL
SELECT [1.5, 1.5, 1.5]::vector;

vector
──────
[1.5, 1.5, 1.5]
```

---

### **`vector cos_distance(vector, vector)`**

Calculate cosine distance between two vectors.

```SQL
SELECT [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector);

cos_distance
────────────
0.481455
```
