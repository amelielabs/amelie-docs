---
weight: 8
title: Monitoring
bookToc: false
---

## Monitoring

The **`amelie top [login] [client options]`** command can be used to get essential system information about the remote
server from the console in real time.

See also [SHOW STATUS](/docs/monitoring/show) and [Monitoring](/docs/monitoring/overview).

---

```sh
# connect to the server using URI without authentication
amelie top --uri="localhost"

uuid:              a23250c4-6363-e01b-9d58-d8277d8f6332
version:           1.0.0
frontends:         5  [51.1, 49.0, 77.7, 81.7, 51.1]
backends:          11 [36.8, 36.8, 36.8, 36.8, 36.8, 36.8, 36.8, 36.8, 36.8, 36.8, 36.8]
memory:            7718 MiB virt / 7043Mib res
connections:       13
sent:              0.046 MiB/sec
recv:              425.858 MiB/sec
write:             325.314 MiB/sec
transactions:      1696 n/sec
ops:               0.589303 millions/sec
wals:              67
checkpoint:        1
lsn:               34279
schemas:           2
tables:            1
tables_shared:     0
secondary indexes: 0
views:             0
```
