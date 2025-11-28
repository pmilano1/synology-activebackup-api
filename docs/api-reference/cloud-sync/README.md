# Cloud Sync APIs

**Category:** Cloud Integration

[← Back to API Reference](../README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## Overview

Cloud Sync APIs provide comprehensive cloud storage synchronization including connections to Google Drive, OneDrive, Dropbox, Amazon S3, and other cloud providers.

---

## API Categories

| Category | Description |
|----------|-------------|
| **[Connections](connections.md)** | Cloud connection management, authentication, status |
| **[Tasks](tasks.md)** | Sync task management, filters, scheduling |

---

## Supported Cloud Providers

- Google Drive
- Microsoft OneDrive
- Dropbox
- Amazon S3
- Backblaze B2
- Google Cloud Storage
- Microsoft Azure
- OpenStack Swift
- WebDAV
- And many more...

---

## Common Parameters

**Session Management:**
- `_sid` - Session ID (required for all APIs)

**Connection Identification:**
- `conn_id` - Connection ID

**Task Identification:**
- `task_id` - Task ID

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid parameter |
| 401 | Unknown error |
| 402 | Cloud Sync not enabled |
| 403 | Permission denied |
| 404 | Connection/task not found |
| 405 | Authentication failed |

---

## Notes

- Cloud Sync package must be installed
- Each cloud provider requires authentication
- Supports bidirectional and unidirectional sync
- File filters can exclude specific files/folders
- Bandwidth throttling available
- Encryption supported for sensitive data

