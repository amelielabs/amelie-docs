---
weight: 11
title: "Crypto"
bookToc: true
---

# Random, Crypto and Hashing Functions

### **`int random()`**

Gen random **`64-bit`** integer.

```SQL
SELECT random();

random
──────
3417165823422050775
```

---

### **`uuid random_uuid()`**

Generate **`uuid`**.

```SQL
SELECT random_uuid();

random_uuid
───────────
829fdbc5-5ad0-85fe-0dda-fedaf323fa9f
```

---

### **`string md5(string)`**

Get MD5 value of the **`string`**.

```SQL
SELECT "hello world"::md5;

md5
───
5eb63bbbe01eeed093cb22bb8f5acdc3
```

---

### **`string sha1(string)`**

Get SHA1 value of the **`string`**.

```SQL
SELECT "hello world"::sha1;

sha1
────
2aae6c35c94fcfb415dbe95f408b9ce91ee846ed
```

---

### **`string jwt(string, string, secret)`**
### **`string jwt(string, obj, secret)`**
### **`string jwt(obj, obj, secret)`**
### **`string jwt(obj, string, secret)`**

Create [JWT](https://jwt.io/) token.

Supported algorithm is only **`HS256`**.

```SQL
SELECT jwt({"alg": "HS256", "typ": "JWT"}, {}, "123");

jwt
───
eyJhbGciOiAiSFMyNTYiLCAidHlwIjogIkpXVCJ9.e30.5gvar2OmXQKJ9rWze2UEo8BZidZjK5B4lMiCnvwZk_4
```
