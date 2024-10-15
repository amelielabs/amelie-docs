---
weight: 8
title: TIMESTAMP
type: docs
bookToc: false
---

## TIMESTAMP

Define a timestamp with timezone according to [ISO8601](https://en.wikipedia.org/wiki/ISO_8601)
with microsecond precision. This type is similar to **`TIMESTAMPTZ`** used by PostgreSQL.

Internally type converted, stored, and operated as a `64-bit` integer representing Unix time in UTC.
All operations are corrected according to the current timezone settings.

**`CURRENT_TIMESTAMP`** and [now()](/docs/sql/functions/timestamp) can be used to get the current transaction time. **`TIMESTAMP`** prefix
before a string can be used to explicitly define timestamp value without convertion.

The type can be used as a key.

---

```SQL
select now(), current_timestamp
["2024-09-26 17:11:03.640011+03", "2024-09-26 17:11:03.640011+03"]

select system.config().timezone
["Asia/Famagusta"]

select current_timestamp - interval '5 hours'
["2024-09-26 12:12:10.684550+03"]

select timestamp "2024-09-26 12:12:10.684550+03"
["2024-09-26 09:12:10.684550+00"]

select "2024-09-26 12:12:10.684550+03"::timestamp
["2024-09-26 09:12:10.684550+00"]

select "2024-09-26 12:12:10.684550+03"::timestamp::int
[1727341930684550]

select 1727341930684550::timestamp
["2024-09-26 12:12:10.684550+03"]

select {"at": now(), "id": system.config().uuid}
[{
  "at": "2024-09-26 16:14:00.722393+03",
  "id": "a74fbf39-cc9d-314e-a33e-3aa47559ffe5"
}]
```

```SQL
create table test (ts timestamp primary key, metrics array)
insert into test values (current_timestamp, [1,2,3])

select * from test
[["2024-09-26 17:13:34.621227+03", [1, 2, 3]]]

set timezone to 'UTC'

select * from test
[["2024-09-26 14:13:34.621227+00", [1, 2, 3]]]
```
