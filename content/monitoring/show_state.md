---
weight: 3
title: "SHOW STATE"
bookToc: false
---

## SHOW STATE Statement

```SQL
SHOW STATE [FORMAT type]
```

Show information about the current system state.

---

```SQL
show state
[{
  "version": "0.1.0",
  "directory": "./repo",
  "uuid": "cd580566-6cf7-fb90-737d-50dd8abdbc79",
  "frontends": 8,
  "backends": 8,
  "checkpoint": 2,
  "lsn": 2,
  "psn": 16,
  "read_only": false
}]

select system.state().version
["0.1.0"]
```
