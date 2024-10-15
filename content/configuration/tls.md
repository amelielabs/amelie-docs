---
weight: 6
title: "TLS"
bookToc: false
---

## TLS Certificates

| Name              | Type     | Mode         | Description |
| :---------------- | :------: | :----:       | :---- |
|  tls_capath      | string | cli | TLS CA directory path. |
|  tls_ca          | string | cli | TLS CA certificate file path. |
|  tls_cert        | string | cli | TLS Server certificate file path. |
|  tls_key         | string | cli | TLS Server certificate private key file path. |

---

```SQL
show tls_cert
[""]

select system.config().tls_cert
[""]
```
