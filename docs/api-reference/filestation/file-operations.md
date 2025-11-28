# FileStation - File Operations

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.CreateFolder

#### Method: `create`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.CreateFolder`
- `version` (required): `2`
- `method` (required): `create`
- `folder_path` (required): Parent folder path (JSON array for multiple)
- `name` (required): Folder name (JSON array for multiple)
- `_sid` (required): Session ID
- `force_parent` (optional): Create parent folders (default: false)
- `additional` (optional): Additional fields

**Response:**
```json
{
  "success": true,
  "data": {
    "folders": [
      {
        "path": "/docker/new_folder",
        "name": "new_folder",
        "isdir": true
      }
    ]
  }
}
```

---

## SYNO.FileStation.Rename

#### Method: `rename`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Rename`
- `version` (required): `2`
- `method` (required): `rename`
- `path` (required): File/folder path (JSON array for multiple)
- `name` (required): New name (JSON array for multiple)
- `_sid` (required): Session ID
- `additional` (optional): Additional fields
- `search_taskid` (optional): Search task ID

**Response:**
```json
{
  "success": true,
  "data": {
    "files": [
      {
        "path": "/docker/new_name.txt",
        "name": "new_name.txt",
        "isdir": false
      }
    ]
  }
}
```

---

## SYNO.FileStation.CopyMove

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.CopyMove`
- `version` (required): `3`
- `method` (required): `start`
- `path` (required): Source path (JSON array for multiple)
- `dest_folder_path` (required): Destination folder
- `_sid` (required): Session ID
- `overwrite` (optional): Overwrite existing (default: false)
- `remove_src` (optional): Move instead of copy (default: false)
- `accurate_progress` (optional): Accurate progress (default: false)
- `search_taskid` (optional): Search task ID

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_CopyMove_12345"
  }
}
```

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.CopyMove`
- `version` (required): `3`
- `method` (required): `status`
- `taskid` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "finished": false,
    "processing_path": "/docker/large_file.bin",
    "progress": 45.5,
    "total": 100,
    "num_processed": 45
  }
}
```

---

#### Method: `stop`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.CopyMove`
- `version` (required): `3`
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

## SYNO.FileStation.Delete

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Delete`
- `version` (required): `2`
- `method` (required): `start`
- `path` (required): File/folder path (JSON array for multiple)
- `_sid` (required): Session ID
- `accurate_progress` (optional): Accurate progress (default: false)
- `recursive` (optional): Delete recursively (default: true)
- `search_taskid` (optional): Search task ID

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_Delete_12345"
  }
}
```

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Delete`
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
    "progress": 100,
    "total": 2,
    "num_processed": 2
  }
}
```

---

#### Method: `stop`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Delete`
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

