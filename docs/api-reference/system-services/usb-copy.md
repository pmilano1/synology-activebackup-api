# System Services - USB Copy

**Category:** Data Management

[← Back to System Services](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.USBCopy

#### Method: `GetSettings`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.USBCopy`
- `version` (required): `1`
- `method` (required): `GetSettings`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "enabled": true,
    "auto_copy": true,
    "destination": "/volume1/usbcopy"
  }
}
```

---

## SYNO.USBCopy.Task

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.USBCopy.Task`
- `version` (required): `1`
- `method` (required): `List`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "tasks": [
      {
        "task_id": 1,
        "name": "Photos Backup",
        "enabled": true,
        "source_filter": "*.jpg,*.png",
        "destination": "/volume1/usbcopy/photos"
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
| `name` | string | Task name |
| `enabled` | boolean | Task enabled |
| `source_filter` | string | File filter pattern |
| `destination` | string | Destination path |

---

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.USBCopy.Task`
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
    "name": "Photos Backup",
    "enabled": true,
    "source_filter": "*.jpg,*.png",
    "destination": "/volume1/usbcopy/photos",
    "overwrite": false,
    "remove_source": false
  }
}
```

---

#### Method: `Enable`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.USBCopy.Task`
- `version` (required): `1`
- `method` (required): `Enable`
- `task_id` (required): Task ID
- `enable` (required): Enable status (true/false)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.USBCopy.Log

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.USBCopy.Log`
- `version` (required): `1`
- `method` (required): `List`
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 200)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "logs": [
      {
        "time": 1732788000,
        "task_id": 1,
        "status": "success",
        "files_copied": 25,
        "bytes_copied": 104857600
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
| `task_id` | integer | Task ID |
| `status` | string | Copy status (`success`, `failed`, `partial`) |
| `files_copied` | integer | Number of files copied |
| `bytes_copied` | integer | Bytes copied |

**Notes:**
- USB Copy package must be installed
- Automatically copies files when USB device is connected
- Supports file filters and destination folders
- Can be triggered manually or automatically
- Logs track all copy operations

