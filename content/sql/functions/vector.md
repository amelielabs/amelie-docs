---
weight: 8
title: "Vector"
bookToc: false
---

## Vector Functions

All vector functions are located in the **`public`** schema, which is default.

### cos_distance(vector, vector)

Calculate cosine distance between two vectors.

```SQL
select [3,2,0,1,4]::vector::cos_distance([1,3,1,2,0]::vector)
[0.481455]
```
