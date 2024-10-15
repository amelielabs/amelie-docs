---
weight: 9
title: Backup and Restore
bookToc: false
---

## Backup and Restore

The **`amelie backup <directory> [login] [client options]`** command can be used to create a hot backup (full copy)
of the remote server repository into the specified directory.

The command is compatible with the [Console Client](/docs/tutorial/cli) options.

After the backup is completed, the new Server can [start](/docs/tutorial/start_stop) using the repository copy.

---

```sh
# do remote server backup
amelie backup ./repo_copy --uri="https://localhost:3485" --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"
amelie start ./repo_copy

# do remote server backup, use saved credentials to connect
amelie login srv --uri="https://localhost:3485" --token="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiAidGVzdCIsICJpYXQiOiAxNzI3OTYyMzU3LCAiZXhwIjogMTczNTkxMTE1N30.79g-77QHd82f7cSbeZSXaz4lP_7F3J4bm7EuZOUCmmM"
amelie backup ./repo_copy srv
```
