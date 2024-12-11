---
weight: 11
title: "Crypto"
bookToc: false
---

## Random, Cryptographic and Hashing Functions

All functions are located in the **`public`** schema, which is default.

---

### **`int random()`**

Gen random **`64-bit`** integer.

```SQL
select random()
[5250487348002782348
```

---

### **`string random_uuid()`**

Generate **`UUID`**.

```SQL
select random_uuid()
["1329e9f0-f52e-25b5-3821-c072f676b461"]
```

---

### **`string md5(string)`**

Get MD5 value of the **`string`**.

```SQL
select "hello world"::md5
["5eb63bbbe01eeed093cb22bb8f5acdc3"]
```

---

### **`string sha1(string)`**

Get SHA1 value of the **`string`**.

```SQL
select "hello world"::sha1
["2aae6c35c94fcfb415dbe95f408b9ce91ee846ed"]
```

---

### **`string jwt(string, string, secret)`**
### **`string jwt(string, obj, secret)`**
### **`string jwt(obj, obj, secret)`**
### **`string jwt(obj, string, secret)`**

Create [JWT](https://jwt.io/) token, which can be used for authentication.

Supported algorithm is only **`HS256`**.

```SQL
select jwt({"alg": "HS256", "typ": "JWT"}, {}, "123")
["eyJhbGciOiAiSFMyNTYiLCAidHlwIjogIkpXVCJ9.e30.5gvar2OmXQKJ9rWze2UEo8BZidZjK5B4lMiCnvwZk_4"]

select jwt({"alg": "HS256", "typ": "JWT"}, {"sub": "1234567890", "name": "John Doe", "iat": 1516239022}, "123")
["eyJhbGciOiAiSFMyNTYiLCAidHlwIjogIkpXVCJ9.eyJzdWIiOiAiMTIzNDU2Nzg5MCIsICJuYW1lIjogIkpvaG4gRG9lIiwgImlhdCI6IDE1MTYyMzkwMjJ9.-BDZCBZz3mjLeTXjKVSla6JRgoWksQA5Ec3_knVZvWA"]
```
