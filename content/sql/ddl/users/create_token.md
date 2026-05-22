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

It is possible to create tokens only for child users or agents (or for any user or agent if called
by the **amelie** superuser).

The server is using internal randomly generated secret to sign and validate server-issued tokens.
The secret is not exposed outside and can be rotated to invalidate all issued tokens.

It is possible to [REVOKE TOKEN](/docs/sql/ddl/users/alter) per a user or agent.

It is possible to invalidate all issued tokens by using the
[ALTER SYSTEM SECRET ROTATE](/docs/sql/ops//system/alter) command.

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
