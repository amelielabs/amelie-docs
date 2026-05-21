---
weight: 14
title: UUID
type: docs
bookToc: true
---

# UUID

**`UUID`** defines an Universally Unique Identifier.

Internally type is converted from string, stored, and operated as a `128-bit` value.
**`UUID`** prefix before a string can be used to define uuid value explicitly.
The type can be used as a part of the primary or secondary key.

**`UUID`** values are comparable.

---

```SQL
SELECT uuid "00000000-0000-0000-0000-000000000000" as id;

id
──
00000000-0000-0000-0000-000000000000

SELECT "00000000-0000-0000-0000-000000000000"::uuid;

uuid
────
00000000-0000-0000-0000-000000000000

SELECT random_uuid();

random_uuid
───────────
5ce51e2e-af77-37e6-29e6-f3a9717ddb6c

SELECT uuid "00000000-0000-0000-0000-000000000000" <
       uuid "00000000-0000-0000-0000-000000000001" as expr;

expr
────
true
```

```SQL
CREATE TABLE example (id uuid primary key using hash);
```
