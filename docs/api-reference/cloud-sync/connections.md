# Cloud Sync - Connections

**Category:** Cloud Integration

[← Back to Cloud Sync](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.CloudSync.Connection

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.CloudSync.Connection`
- `version` (required): `1`
- `method` (required): `List`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "connections": [
      {
        "conn_id": 1,
        "cloud_type": "gdrive",
        "display_name": "My Google Drive",
        "status": "connected",
        "account": "user@gmail.com"
      }
    ],
    "total": 1
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `conn_id` | integer | Connection ID |
| `cloud_type` | string | Cloud provider type |
| `display_name` | string | Connection display name |
| `status` | string | Connection status (`connected`, `disconnected`, `error`) |
| `account` | string | Cloud account identifier |

**Cloud Types:**
- `gdrive` - Google Drive
- `onedrive` - Microsoft OneDrive
- `dropbox` - Dropbox
- `s3` - Amazon S3
- `b2` - Backblaze B2
- `gcs` - Google Cloud Storage
- `azure` - Microsoft Azure

---

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.CloudSync.Connection`
- `version` (required): `1`
- `method` (required): `Get`
- `conn_id` (required): Connection ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "conn_id": 1,
    "cloud_type": "gdrive",
    "display_name": "My Google Drive",
    "status": "connected",
    "account": "user@gmail.com",
    "quota_total": 17179869184,
    "quota_used": 5368709120
  }
}
```

---

#### Method: `Pause`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.CloudSync.Connection`
- `version` (required): `1`
- `method` (required): `Pause`
- `conn_id` (required): Connection ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

**Notes:**
- Pauses all sync tasks for this connection
- Does not disconnect from cloud provider

---

#### Method: `Resume`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.CloudSync.Connection`
- `version` (required): `1`
- `method` (required): `Resume`
- `conn_id` (required): Connection ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.CloudSync.Connection.Log

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.CloudSync.Connection.Log`
- `version` (required): `1`
- `method` (required): `List`
- `conn_id` (required): Connection ID
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 100)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "logs": [
      {
        "time": 1732788000,
        "type": "info",
        "message": "Sync completed successfully"
      }
    ],
    "total": 1
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `time` | integer | Log timestamp (Unix time) |
| `type` | string | Log type (`info`, `warning`, `error`) |
| `message` | string | Log message |

**Notes:**
- Connection logs track sync activity and errors
- Useful for troubleshooting sync issues
- Logs are retained for limited time

