# FileStation API Reference

[← Back to API Reference](../README.md)

---

## Overview

FileStation provides comprehensive file management capabilities for Synology NAS, including file operations, uploads, downloads, sharing, compression, and search functionality.

**Base Path:** `/webapi/entry.cgi`

**Authentication:** Session ID (`_sid`) required for all operations

---

## API Categories

| Category | APIs | Description |
|----------|------|-------------|
| **[Info & Listing](info-listing.md)** | 4 | Get FileStation info, list shares, list files, get file info |
| **[Search](search.md)** | 4 | Start search, get results, stop search tasks |
| **[Favorites](favorites.md)** | 6 | Manage favorite folders |
| **[File Operations](file-operations.md)** | 8 | Create, rename, copy, move, delete files/folders |
| **[Upload & Download](upload-download.md)** | 3 | Upload files, download files, check permissions |
| **[Sharing](sharing.md)** | 6 | Create/manage shared links |
| **[Compression](compression.md)** | 6 | Compress/extract archives |
| **[Background Tasks](background-tasks.md)** | 9 | Manage long-running operations |

---

## Quick Start

### 1. Get FileStation Info

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.Info" \
  -d "version=2" \
  -d "method=get" \
  -d "_sid=YOUR_SESSION_ID"
```

### 2. List Shared Folders

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.List" \
  -d "version=2" \
  -d "method=list_share" \
  -d "_sid=YOUR_SESSION_ID"
```

### 3. List Files in a Folder

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.List" \
  -d "version=2" \
  -d "method=list" \
  -d "folder_path=/home" \
  -d "_sid=YOUR_SESSION_ID"
```

### 4. Upload a File

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -F "api=SYNO.FileStation.Upload" \
  -F "version=2" \
  -F "method=upload" \
  -F "path=/home" \
  -F "create_parents=true" \
  -F "overwrite=true" \
  -F "file=@/path/to/local/file.txt" \
  -F "_sid=YOUR_SESSION_ID"
```

### 5. Create a Shared Link

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.Sharing" \
  -d "version=3" \
  -d "method=create" \
  -d "path=/home/document.pdf" \
  -d "_sid=YOUR_SESSION_ID"
```

---

## Common Parameters

### Pagination

| Parameter | Type | Description |
|-----------|------|-------------|
| `offset` | Integer | Starting index (0-based) |
| `limit` | Integer | Maximum number of results |

### Sorting

| Parameter | Type | Description |
|-----------|------|-------------|
| `sort_by` | String | Field to sort by (name, size, mtime, etc.) |
| `sort_direction` | String | `asc` or `desc` |

### Additional Info

| Parameter | Type | Description |
|-----------|------|-------------|
| `additional` | String/Array | Comma-separated list of additional fields to return |

**Available Additional Fields:**
- `real_path` - Real path in file system
- `size` - File size
- `owner` - Owner information
- `time` - Time information (atime, mtime, ctime, crtime)
- `perm` - Permission information
- `mount_point_type` - Mount point type
- `type` - File type

---

## Response Format

All FileStation APIs return JSON responses in this format:

```json
{
  "success": true,
  "data": {
    // API-specific data
  }
}
```

**Error Response:**
```json
{
  "success": false,
  "error": {
    "code": 400
  }
}
```

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid parameter |
| 401 | No such file or directory |
| 402 | System is too busy |
| 403 | Invalid user |
| 404 | Invalid group |
| 405 | Invalid user and group |
| 406 | Can't get user/group information from the account server |
| 407 | Operation not permitted |
| 408 | No such task of the file operation |
| 409 | Non-supported file system |
| 410 | Failed to connect internet-based file system (ex: CIFS) |
| 411 | Read-only file system |
| 412 | Filename too long in the non-encrypted file system |
| 413 | Filename too long in the encrypted file system |
| 414 | File already exists |
| 415 | Disk quota exceeded |
| 416 | No space left on device |
| 417 | Input/output error |
| 418 | Illegal name or path |
| 419 | Illegal file name |
| 420 | Illegal file name on FAT file system |
| 421 | Device or resource busy |

---

## See Also

- [Info & Listing APIs](info-listing.md)
- [Search APIs](search.md)
- [File Operations APIs](file-operations.md)
- [Upload & Download APIs](upload-download.md)
- [Sharing APIs](sharing.md)

