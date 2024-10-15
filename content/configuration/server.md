---
weight: 7
title: "Server"
bookToc: false
---

## Server Settings

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
| listen            |  array   | cli          | Listen for incoming connections |

Listen represent an array of objects, where following fields are recognized:

| Argument             | Type | Description |
| :----------------    |  :----:  | :----      |
|  path            | string | Unix socket file path. |
|  path_mode       | string | Unix socket file mode. |
|  host            | string | Listen address (using **`host`** or **`path`** is mandatory). |
|  port            | int    | Listen port. |
|  tls             | bool    | Enable TLS for this address. |
|  auth            | bool    | Enable Authentication for this address. |

---


```SQL
show listen
[{
  "host": "*",
  "port": 3485,
  "auth": true,
  "tls": true
}]

select system.config().listen
[{
  "host": "*",
  "port": 3485,
  "auth": true,
  "tls": true
}]
```
