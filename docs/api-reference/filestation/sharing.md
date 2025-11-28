# FileStation - Sharing

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.Sharing

#### Method: `getinfo`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Sharing`
- `version` (required): `3`
- `method` (required): `getinfo`
- `id` (required): Shared link ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "links": [
      {
        "id": "SHARE_LINK_ID",
        "url": "https://nas.example.com/sharing/SHARE_LINK_ID",
        "link_owner": "admin",
        "path": "/docker/document.pdf",
        "date_expired": 0,
        "date_available": 0,
        "status": "valid",
        "has_password": false,
        "expire_times": 0,
        "access_time": 5,
        "isFolder": false
      }
    ]
  }
}
```

---

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Sharing`
- `version` (required): `3`
- `method` (required): `list`
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results
- `sort_by` (optional): Sort field: `name`, `user`, `access_time`, `mtime`, `expire_time`, `status`
- `sort_direction` (optional): `asc` or `desc`
- `force_clean` (optional): Clean invalid links first (default: false)

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 3,
    "offset": 0,
    "links": [
      {
        "id": "LINK_001",
        "url": "https://nas.example.com/sharing/LINK_001",
        "link_owner": "admin",
        "path": "/docker/README.md",
        "date_expired": 0,
        "status": "valid",
        "has_password": false,
        "access_time": 12,
        "isFolder": false
      }
    ]
  }
}
```

---

#### Method: `create`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Sharing`
- `version` (required): `3`
- `method` (required): `create`
- `path` (required): File/folder path to share
- `_sid` (required): Session ID
- `password` (optional): Password protection
- `date_expired` (optional): Expiration date (Unix timestamp, 0 = never)
- `date_available` (optional): Available from date (Unix timestamp, 0 = immediate)
- `expire_times` (optional): Max accesses (0 = unlimited)

**Response:**
```json
{
  "success": true,
  "data": {
    "links": [
      {
        "id": "NEW_LINK_ID",
        "url": "https://nas.example.com/sharing/NEW_LINK_ID",
        "link_owner": "admin",
        "path": "/docker/document.pdf",
        "date_expired": 1735689600,
        "status": "valid",
        "has_password": true,
        "expire_times": 10,
        "isFolder": false
      }
    ]
  }
}
```

---

#### Method: `delete`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Sharing`
- `version` (required): `3`
- `method` (required): `delete`
- `id` (required): Link ID (comma-separated for multiple)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `clear_invalid`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Sharing`
- `version` (required): `3`
- `method` (required): `clear_invalid`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `edit`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Sharing`
- `version` (required): `3`
- `method` (required): `edit`
- `id` (required): Link ID
- `_sid` (required): Session ID
- `password` (optional): New password (empty to remove)
- `date_expired` (optional): New expiration date
- `date_available` (optional): New available from date
- `expire_times` (optional): New max accesses

**Response:**
```json
{
  "success": true,
  "data": {
    "links": [
      {
        "id": "LINK_ID",
        "url": "https://nas.example.com/sharing/LINK_ID",
        "link_owner": "admin",
        "path": "/docker/document.pdf",
        "date_expired": 1767225600,
        "has_password": true
      }
    ]
  }
}
```

