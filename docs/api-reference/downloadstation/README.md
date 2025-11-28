# DownloadStation

**Category:** Download Management

[← Back to API Reference](../README.md)

---

**Endpoint:** `/webapi/entry.cgi`

**Authentication:** Session ID (`_sid`) required for all operations

---

## API Categories

| Category | Description |
|----------|-------------|
| **[Info & Config](info-config.md)** | Get/set DownloadStation info and configuration |
| **[Tasks](tasks.md)** | Manage download tasks (list, create, delete, pause, resume) |
| **[Statistics](statistics.md)** | Get download statistics |
| **[RSS](rss.md)** | Manage RSS feeds |
| **[BT Search](bt-search.md)** | BitTorrent search functionality |

---

## Common Parameters

**Task Additional Fields:**
- `detail` - Detailed task information
- `transfer` - Transfer statistics
- `file` - File list
- `tracker` - Tracker information
- `peer` - Peer information

**Task Status:**
- `waiting` - Task is waiting
- `downloading` - Task is downloading
- `paused` - Task is paused
- `finishing` - Task is finishing
- `finished` - Task is finished
- `hash_checking` - Hash checking
- `seeding` - Seeding (BitTorrent)
- `filehosting_waiting` - Waiting for file hosting
- `extracting` - Extracting files
- `error` - Error occurred

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid parameter |
| 401 | Invalid task ID |
| 402 | Invalid task action |
| 403 | Invalid file format |
| 404 | File upload failed |
| 405 | Timeout |

---

## Notes

- All download tasks are identified by unique task IDs
- BitTorrent tasks support seeding after completion
- RSS feeds can be configured for automatic downloads
- Download speeds are in KB/s

