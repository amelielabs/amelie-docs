---
weight: 5
title: HTTP API
bookToc: false
---

## HTTP Request

Currently, the Server accepts only **`HTTP/1.1`** plain text **`SQL`** commands directly using the **`POST /`** method.

### **`POST / (application/text)`**

```http
POST / HTTP/1.1
Host: localhost:3485
Content-Type: application/text
Content-Length: 22

SELECT "hello, world!"
```

```sh
curl -X POST \
-H "Content-Type: application/text" \
-d 'SELECT "hello, world!"' \
http://localhost:3485/
["hello, world!"]
```

### Authentication

Amelie authentication is based on using **`JSON Web Tokens`** ([JWT](https://jwt.io/)).

If authentication is enabled, the incoming HTTP request header must include the **`Authorization`** field with
a valid JWT token in the format: **`Authentication: Bearer <JWT>`**.

JWT-based authentication must be used only with **`HTTPS`** connections.

```sh
curl -X POST \
-H "Authorization: Bearer <JWT>" \
-H "Content-Type: application/text" \
-d 'SELECT "hello, world!"' \
--cacert ca.crt \
https://localhost:3485/
["hello, world!"]
```

Learn more about [Authentication](/docs/tutorial/auth).

---

## HTTP Reply

Currently, the Server responds using **`application/json`**.
Based on the request result, the Server responds with the following status codes:

### **`200 OK`**

On successful execution, the Server will respond with status code `200`, containing a
JSON array with zero or more values:

```http
HTTP/1.1 200 OK
Content-Length: 17
Content-Type: application/json

["hello, world!"]
```

### **`204 No Content`**

On successful execution, the Server will respond with status code `204` if the result does not have data.

```http
HTTP/1.1 204 No Content
```

### **`400 Bad Request`**

In case of an error, the server will respond with status code `400`, containing a single JSON object:

```http
HTTP/1.1 400 Bad Request
Content-Length: 41
Content-Type: application/json

{"code": 1, "msg": "unterminated string"}
```

### **`403 Forbidden`**

In case of authentication errors, the server will respond with the status code `403` without
data and close the client connection.

```http
HTTP/1.1 403 Forbidden
```
