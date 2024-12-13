---
weight: 9
title: "Math"
bookToc: false
---

## Mathematical Functions

All math functions are located in the **`public`** schema, which is default.

---

### **`any greatest(...)`**

Compare arguments and return max.

```SQL
select greatest(1,2,3);
[3]
```

---

### **`any least(...)`**

Compare arguments and return min.

```SQL
select least(1,2,3);
[1]
```

---

### **`int abs(int)`**
### **`double fabs(double)`**

Compute absolute value of the integer or double.

```SQL
select (-63)::abs;
[63]
```

---

### **`int round(double)`**

Round **`double`** value and return int.

```SQL
select 3.14::round;
[3]
```

---

### **`int sign(arg)`**

Return **`-1, 0`** or **`1`** depending of the **`int`** or **`double`** sign.

```SQL
select -3::sign;
[-1]

select 0::sign;
[0]
```

---

### **`double ceil(double)`**

Return the smallest int value not less than argument.

```SQL
select 3.14::ceil;
[4]
```

---

### **`double exp(double)`**

Returns the natural exponential of the value.

```SQL
select exp(1.0);
[2.71828]
```

---

### **`double floor(double)`**

Return the largest int value, which is not greater than the argument.

```SQL
select 3.14::floor;
[3]
```

---

### **`int mod(int, int)`**
### **`double fmod(double, double)`**

Get the remainder after division. Supported types are **`int`** and **`double`**.

```SQL
select mod(9, 4);
[1]

select fmod(30.0, 3.6);
[1.2]
```

---

### **`int pow(int, int)`**
### **`double fpow(double, double)`**

Return the value of x raised to the power of y.
Supported types are **`int`** and **`double`**.

```SQL
select pow(9, 3);
[729]

select fpow(9.1, 3.2);
[1172.01]
```

---

### **`double trunc(double)`**

Round to the nearest int value that is not larger in magnitude.

```SQL
select trunc(42.8);
[42]

select trunc(-48.8023);
[-48]
```

---

### **`double pi()`**

Return the value of PI.

```SQL
select pi();
[3.14159]
```

---

### **`double sqrt(arg)`**

Return non-negative square root of the argument.
Supported types are **`int`** and **`double`**.

```SQL
select sqrt(2);
[1.41421]
```

---

### **`double acos(arg)`**

Return the arc cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select acos(1);
[0]
```

---

### **`double acosh(arg)`**

Return the the inverse hyperbolic cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select acosh(1);
[0]
```

---

### **`double asin(arg)`**

Return the arc sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select asin(1);
[1.5708]
```

---

### **`double asinh(arg)`**

Return the inverse hyperbolic sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select asinh(1);
[0.881374]
```

---

### **`double atan(arg)`**

Return the arc tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
select atan(1);
[0.785398]
```

---

### **`double atanh(arg)`**

Return the inverse hyperbolic tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
select atanh(0.5);
[0.549306]
```

---

### **`double atan2(y, x)`**

Return the principal value of the arc tangent of **`y / x`**, using the signs of the two
arguments to determine the quadrant of the result. Supported types are **`int`** and **`double`**.

```SQL
select atan2(1, 0);
[1.5708]
```

---

### **`double cos(arg)`**

Return the cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select cos(1);
[0.540302]
```

---

### **`double cosh(arg)`**

Return the hyperbolic cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select cosh(1);
[1.54308]
```

---

### **`double sin(arg)`**

Return the sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select sin(1);
[0.841471]
```

---

### **`double sinh(arg)`**

Return the hyperbolic sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
select sin(1);
[1.1752]
```

---

### **`double tan(arg)`**

Return the tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
select tan(1);
[1.55741]
```

---

### **`double tanh(arg)`**

Return the hyperbolic tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
select tanh(1);
[0.761594]
```

---

### **`double ln(arg)`**

Return the natural logarithm on the argument. Supported types are **`int`** and **`double`**.

```SQL
select ln(2.0);
[0.693147]
```

---

### **`double log(arg)`**
### **`double log10(arg)`**

Return the base 10 logarithm of the argument. Supported types are **`int`** and **`double`**.

```SQL
select log(1000);
```

---

### **`double log2(arg)`**

Return the base 2 logarithm of the argument. Supported types are **`int`** and **`double`**.

```SQL
select log2(16);
[4]
```
