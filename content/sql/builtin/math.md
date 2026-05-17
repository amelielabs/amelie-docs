---
weight: 9
title: "Math"
bookToc: true
---

# Mathematical Functions

### **`any greatest(...)`**

Compare arguments and return max.

```SQL
SELECT greatest(1,2,3);

greatest
────────
3
```

---

### **`any least(...)`**

Compare arguments and return min.

```SQL
SELECT least(1,2,3);

least
─────
1
```

---

### **`int abs(int)`**
### **`double fabs(double)`**

Compute absolute value of the integer or double.

```SQL
SELECT (-63)::abs;

abs
───
63
```

---

### **`int round(double)`**

Round **`double`** value and return int.

```SQL
SELECT 3.14::round;

round
─────
3
```

---

### **`int sign(arg)`**

Return **`-1, 0`** or **`1`** depending of the **`int`** or **`double`** sign.

```SQL
SELECT -3::sign;

sign
────
-1

SELECT 0::sign;

sign
────
0
```

---

### **`double ceil(double)`**

Return the smallest int value not less than argument.

```SQL
SELECT 3.14::ceil;

ceil
────
4
```

---

### **`double exp(double)`**

Returns the natural exponential of the value.

```SQL
SELECT exp(1.0);

exp
───
2.71828
```

---

### **`double floor(double)`**

Return the largest int value, which is not greater than the argument.

```SQL
SELECT 3.14::floor;

floor
─────
3
```

---

### **`int mod(int, int)`**
### **`double fmod(double, double)`**

Get the remainder after division. Supported types are **`int`** and **`double`**.

```SQL
SELECT mod(9, 4);

mod
───
1

SELECT fmod(30.0, 3.6);

fmod
────
1.2
```

---

### **`int pow(int, int)`**
### **`double fpow(double, double)`**

Return the value of x raised to the power of y.
Supported types are **`int`** and **`double`**.

```SQL
SELECT pow(9, 3);

pow
───
729

SELECT fpow(9.1, 3.2);

fpow
────
1172.01
```

---

### **`double trunc(double)`**

Round to the nearest int value that is not larger in magnitude.

```SQL
SELECT trunc(42.8);

trunc
─────
42

SELECT trunc(-48.8023);

trunc
─────
-48
```

---

### **`double pi()`**

Return the value of PI.

```SQL
SELECT pi();

pi
──
3.14159
```

---

### **`double sqrt(arg)`**

Return non-negative square root of the argument.
Supported types are **`int`** and **`double`**.

```SQL
SELECT sqrt(2);

sqrt
────
1.41421
```

---

### **`double acos(arg)`**

Return the arc cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT acos(1);

acos
────
0
```

---

### **`double acosh(arg)`**

Return the the inverse hyperbolic cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT acosh(1);

acosh
─────
0
```

---

### **`double asin(arg)`**

Return the arc sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT asin(1);

asin
────
1.5708
```

---

### **`double asinh(arg)`**

Return the inverse hyperbolic sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT asinh(1);

asinh
─────
0.881374
```

---

### **`double atan(arg)`**

Return the arc tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT atan(1);

atan
────
0.785398
```

---

### **`double atanh(arg)`**

Return the inverse hyperbolic tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT atanh(0.5);

atanh
─────
0.549306
```

---

### **`double atan2(y, x)`**

Return the principal value of the arc tangent of **`y / x`**, using the signs of the two
arguments to determine the quadrant of the result. Supported types are **`int`** and **`double`**.

```SQL
SELECT atan2(1, 0);

atan2
─────
1.5708
```

---

### **`double cos(arg)`**

Return the cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT cos(1);

cos
───
0.540302
```

---

### **`double cosh(arg)`**

Return the hyperbolic cosine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT cosh(1);

cosh
────
1.54308
```

---

### **`double sin(arg)`**

Return the sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT sin(1);

sin
───
0.841471
```

---

### **`double sinh(arg)`**

Return the hyperbolic sine of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT sinh(1);

sinh
────
1.1752
```

---

### **`double tan(arg)`**

Return the tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT tan(1);

tan
───
1.55741
```

---

### **`double tanh(arg)`**

Return the hyperbolic tangent of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT tanh(1);

tanh
────
0.761594
```

---

### **`double ln(arg)`**

Return the natural logarithm on the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT ln(2.0);

ln
──
0.693147
```

---

### **`double log(arg)`**
### **`double log10(arg)`**

Return the base 10 logarithm of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT log(1000);

log
───
3
```

---

### **`double log2(arg)`**

Return the base 2 logarithm of the argument. Supported types are **`int`** and **`double`**.

```SQL
SELECT log2(16);

log2
────
4
```
