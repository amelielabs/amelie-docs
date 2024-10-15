---
weight: 10
title: "Encoding"
bookToc: false
---

## Functions for Data Encoding

All encoding functions are located in the **`public`** schema, which is default.

### encode(string, encoding)

Encode the **`string`** using the specified **`encoding`**.

Supported encodings are:

* **`base64`**
* **`base64url`**

```SQL
select {"data": [1,2,3]}::string::encode("base64")
["eyJkYXRhIjogWzEsIDIsIDNdfQ=="]
```

### decode(string, encoding)

Decode the **`string`** using the specified **`encoding`**.

Supported encodings are:

* **`base64`**
* **`base64url`**

```SQL
select "eyJkYXRhIjogWzEsIDIsIDNdfQ=="::decode("base64")::native
[{
  "data": [1, 2, 3]
}]
```
