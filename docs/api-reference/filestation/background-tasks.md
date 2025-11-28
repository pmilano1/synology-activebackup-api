# FileStation - Background Tasks

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.BackgroundTask

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.BackgroundTask`
- `version` (required): `3`
- `method` (required): `list`
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results
- `sort_by` (optional): Sort field
- `sort_direction` (optional): `asc` or `desc`
- `api_filter` (optional): Filter by API (JSON array)

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 3,
    "offset": 0,
    "tasks": [
      {
        "taskid": "FileStation_CopyMove_12345",
        "api": "SYNO.FileStation.CopyMove",
        "method": "start",
        "finished": false,
        "progress": 45.5
      }
    ]
  }
}
```

---

## SYNO.FileStation.DirSize

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.DirSize`
- `version` (required): `2`
- `method` (required): `start`
- `path` (required): Directory path (JSON array for multiple)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_DirSize_12345"
  }
}
```

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.DirSize`
- `version` (required): `2`
- `method` (required): `status`
- `taskid` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "finished": true,
    "total_size": 1073741824,
    "num_dirs": 150,
    "num_files": 2500
  }
}
```

---

#### Method: `stop`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.DirSize`
- `version` (required): `2`
- `method` (required): `stop`
- `taskid` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.FileStation.MD5

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.MD5`
- `version` (required): `2`
- `method` (required): `start`
- `file_path` (required): File path
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_MD5_12345"
  }
}
```

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.MD5`
- `version` (required): `2`
- `method` (required): `status`
- `taskid` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "finished": true,
    "md5": "5d41402abc4b2a76b9719d911017c592"
  }
}
```

---

#### Method: `stop`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.MD5`
- `version` (required): `2`
- `method` (required): `stop`
- `taskid` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

