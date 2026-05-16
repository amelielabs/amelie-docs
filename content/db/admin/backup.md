---
weight: 9
title: Backup and Restore
bookToc: true
---

# Backup and Restore

The **`amelie backup <directory> [options]`** command can be used to create a hot backup
of the remote server repository into the specified directory.

The command is compatible with the [Console Client](/docs/db/admin/cli) options.

After the backup is completed, the new server can [start](/docs/db/admin/start_stop) using the repository copy.

---

```sh
# do remote server backup
amelie backup ./backup http://localhost
amelie start ./backup

# do remote server backup, use saved credentials to connect
amelie bookmark home https://localhost --token="..."
amelie backup ./backup home
```
