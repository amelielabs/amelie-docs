---
weight: 4
title: "CREATE TOKEN"
bookToc: true
---

# CREATE TOKEN

```SQL
CREATE TOKEN user_name [EXPIRE interval]
```

Create an authentication token (JWT) for the existing user that will expire in a given
interval. If the interval is not defined, **`1 day`** will be set automatically.

---

```SQL
CREATE TOKEN test EXPIRE '5 min';

test
────
"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzc5MTAyMjcxLCAiZXhwIjogMTc3OTEwMjU3MX0.Zfk1N6_myn1Wgb7xlARD2TozkoVYQOmfbPh8wNruxDY"
```

```sh
# connect to the remote server
amelie https://<address>:<port> --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzc5MTAyMjcxLCAiZXhwIjogMTc3OTEwMjU3MX0.Zfk1N6_myn1Wgb7xlARD2TozkoVYQOmfbPh8wNruxDY"
```
