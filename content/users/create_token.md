---
weight: 2
title: "CREATE TOKEN"
bookToc: false
---

## CREATE TOKEN Statement

```SQL
CREATE TOKEN user_name [EXPIRE interval]
```

Create an authentication token (JWT) for the existing user that will expire in a given
interval. If the interval is not defined, **`1 year`** will be set automatically.

---

```SQL
create user test secret 'test';

create token test expire '3 month';
["eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"]
```

```sh
# connect to the server, using previously generated token by the server
amelie --uri="https://localhost:3485" --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"

# connect to the server, CLI will generate one-time JWT token each time automatically
amelie --uri="https://localhost:3485" --user="test" --secret="test"

# connect to the server, using saved credentials, CLI will generate and save JWT token
amelie login home --uri="https://localhost:3485" --user="test" --secret="test"
amelie home

# connect to the server, using saved credentials
amelie login home --uri="https://localhost:3485" --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"
amelie home
```
