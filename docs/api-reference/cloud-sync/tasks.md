# Cloud Sync - Tasks

**Category:** Cloud Integration

[← Back to Cloud Sync](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.CloudSync.Task

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.CloudSync.Task`
- `version` (required): `1`
- `method` (required): `List`
- `conn_id` (optional): Filter by connection ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "tasks": [
      {
        "task_id": 1,
        "conn_id": 1,
        "name": "Documents Sync",
        "local_path": "/volume1/Documents",
        "remote_path": "/Documents",
        "direction": "bidirectional",
        "status": "syncing",
        "progress": 45
      }
    ],
    "total": 1
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `task_id` | integer | Task ID |
| `conn_id` | integer | Connection ID |
| `name` | string | Task name |
| `local_path` | string | Local folder path |
| `remote_path` | string | Remote folder path |
| `direction` | string | Sync direction |
| `status` | string | Task status |
| `progress` | integer | Sync progress (0-100) |

**Sync Directions:**
- `bidirectional` - Two-way sync
- `upload` - Local to cloud only
- `download` - Cloud to local only

**Task Status:**
- `idle` - Not syncing
- `syncing` - Currently syncing
- `paused` - Paused
- `error` - Error occurred

---

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.CloudSync.Task`
- `version` (required): `1`
- `method` (required): `Get`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "task_id": 1,
    "conn_id": 1,
    "name": "Documents Sync",
    "local_path": "/volume1/Documents",
    "remote_path": "/Documents",
    "direction": "bidirectional",
    "status": "syncing",
    "progress": 45,
    "files_synced": 150,
    "bytes_synced": 104857600,
    "last_sync_time": 1732788000
  }
}
```

---

#### Method: `Pause`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.CloudSync.Task`
- `version` (required): `1`
- `method` (required): `Pause`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `Resume`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.CloudSync.Task`
- `version` (required): `1`
- `method` (required): `Resume`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.CloudSync.Task.Filter

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.CloudSync.Task.Filter`
- `version` (required): `1`
- `method` (required): `Get`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "filters": [
      {
        "type": "exclude",
        "pattern": "*.tmp"
      },
      {
        "type": "exclude",
        "pattern": ".DS_Store"
      }
    ]
  }
}
```

**Filter Types:**
- `exclude` - Exclude matching files
- `include` - Include only matching files

**Notes:**
- Filters use wildcard patterns (`*`, `?`)
- Multiple filters can be applied
- Filters apply to both upload and download
- Common exclusions: temp files, system files, cache

