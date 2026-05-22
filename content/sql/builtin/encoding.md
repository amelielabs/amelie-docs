---
weight: 10
title: "Encoding"
bookToc: true
---

# Data Encoding Functions

### **`string encode(string, encoding)`**

Encode the **`string`** using the specified **`encoding`**.

Supported encodings are:

* **`base64`**
* **`base64url`**

```SQL
SELECT {"data": [1,2,3]}::string::encode("base64");

encode
──────
eyJkYXRhIjogWzEsIDIsIDNdfQ==
```

---

### **`string decode(string, encoding)`**

Decode the **`string`** using the specified **`encoding`**.

Supported encodings are:

* **`base64`**
* **`base64url`**

```SQL
SELECT "eyJkYXRhIjogWzEsIDIsIDNdfQ=="::decode("base64")::json_decode;

json_decode
───────────
{
  "data": [1, 2, 3]
}
```
