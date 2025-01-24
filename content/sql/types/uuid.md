---
weight: 14
title: UUID
type: docs
bookToc: false
---

## UUID

**`UUID`** defines an Universally Unique Identifier.

Internally type is converted from string, stored, and operated as a `128-bit` value.
**`UUID`** prefix before a string can be used to define uuid value explicitly.
The type can be used as a part of the primary or secondary key.

**`UUID`** values are comparable.

---

```SQL
select uuid "00000000-0000-0000-0000-000000000000";
["00000000-0000-0000-0000-000000000000"]

select "00000000-0000-0000-0000-000000000000"::uuid;
["00000000-0000-0000-0000-000000000000"]

select random_uuid();
["4845888e-dbc4-88bc-2e22-9673ccd23bee"]

select uuid "00000000-0000-0000-0000-000000000000" <
       uuid "00000000-0000-0000-0000-000000000001";
[true]
```

```SQL
create table example (id uuid primary key) with (type = 'hash')
insert into example values ("00000000-0000-0000-0000-000000000000")
insert into example values ("00000000-0000-0000-0000-000000000001")
insert into example values ("00000000-0000-0000-0000-000000000002")
select * from example order by id
["00000000-0000-0000-0000-000000000000", "00000000-0000-0000-0000-000000000001",
 "00000000-0000-0000-0000-000000000002"]
```
