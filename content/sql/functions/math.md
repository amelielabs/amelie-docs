---
weight: 8
title: "Math"
bookToc: false
---

## Mathematical Functions

All math functions are located in the **`public`** schema, which is default.

### greatest(...)

Compare arguments and return max.

```SQL
select greatest(1,2,3)
[3]
```

---

### least(...)

Compare arguments and return min.

```SQL
select least(1,2,3)
[1]
```

---

### abs(arg)

Compute absolute value of the integer or real.

```SQL
select (-63)::abs
[63]
```

---

### round(real)

Round **`real`** value and return int.

```SQL
select 3.14::round
[3]
```

---

### sign(arg)

Return **`-1, 0`** or **`1`** depending of the **`int`** or **`real`** sign.

```SQL
select -3::sign
[-1]

select 0::sign
[0]
```

---

### ceil(real)

Return the smallest int value not less than argument.

```SQL
select 3.14::ceil
[4]
```

---

### exp(real)

Returns the natural exponential of the value.

```SQL
select exp(1.0)
[2.71828]
```

---

### floor(real)

Return the largest int value, which is not greater than the argument.

```SQL
select 3.14::floor
[3]
```

---

### mod(arg, arg)

Get the remainder after division. Supported types are **`int`** and **`real`**.

```SQL
select mod(9, 4)
[1]

select mod(30.0, 3.6)
[1.2]
```

---

### power(x, y)

Return the value of x raised to the power of y.
Supported types are **`int`** and **`real`**.

```SQL
select power(9, 3)
[729]

select power(9.1, 3.2)
[1172.01]
```

---

### trunc(real)

Round to the nearest int value that is not larger in magnitude.

```SQL
select trunc(42.8)
[42]

select trunc(-48.8023)
[-48]
```

---

### pi()

Return the value of PI.

```SQL
select pi()
[3.14159]
```

---

### sqrt(arg)

Return non-negative square root of the argument.
Supported types are **`int`** and **`real`**.

```SQL
select sqrt(2)
[1.41421]
```

---

### acos(arg)

Return the arc cosine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select acos(1)
[0]
```

---

### acosh(arg)

Return the the inverse hyperbolic cosine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select acosh(1)
[0]
```

---

### asin(arg)

Return the arc sine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select asin(1)
[1.5708]
```

---

### asinh(arg)

Return the inverse hyperbolic sine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select asinh(1)
[0.881374]
```

---

### atan(arg)

Return the arc tangent of the argument. Supported types are **`int`** and **`real`**.

```SQL
select atan(1)
[0.785398]
```

---

### atanh(arg)

Return the inverse hyperbolic tangent of the argument. Supported types are **`int`** and **`real`**.

```SQL
select atanh(0.5)
[0.549306]
```

---

### atan2(y, x)

Return the principal value of the arc tangent of **`y / x`**, using the signs of the two
arguments to determine the quadrant of the result. Supported types are **`int`** and **`real`**.

```SQL
select atan2(1, 0)
[1.5708]
```

---

### cos(arg)

Return the cosine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select cos(1)
[0.540302]
```

---

### cosh(arg)

Return the hyperbolic cosine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select cosh(1)
[1.54308]
```

---

### sin(arg)

Return the sine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select sin(1)
[0.841471]
```

---

### sinh(arg)

Return the hyperbolic sine of the argument. Supported types are **`int`** and **`real`**.

```SQL
select sin(1)
[1.1752]
```

---

### tan(arg)

Return the tangent of the argument. Supported types are **`int`** and **`real`**.

```SQL
select tan(1)
[1.55741]
```

---

### tanh(arg)

Return the hyperbolic tangent of the argument. Supported types are **`int`** and **`real`**.

```SQL
select tanh(1)
[0.761594]
```

---

### ln(arg)

Return the natural logarithm on the argument. Supported types are **`int`** and **`real`**.

```SQL
select ln(2.0)
[0.693147]
```

---

### log(arg)
### log10(arg)

Return the base 10 logarithm of the argument. Supported types are **`int`** and **`real`**.

```SQL
select log(1000)
```

---

### log2(arg)

Return the base 2 logarithm of the argument. Supported types are **`int`** and **`real`**.

```SQL
select log2(16)
[4]
```
