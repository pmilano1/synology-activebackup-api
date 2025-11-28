# FileStation - File Operations APIs

[← Back to FileStation](README.md)

---

## SYNO.FileStation.CreateFolder

Create one or more folders.

**API:** `SYNO.FileStation.CreateFolder`  
**Version:** 2  
**Method:** `create`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `folder_path` | String/Array | Yes | Parent folder path(s) - JSON array for multiple |
| `name` | String/Array | Yes | Folder name(s) - JSON array for multiple |
| `force_parent` | Boolean | No | Create parent folders if they don't exist (default: false) |
| `additional` | String/Array | No | Additional info to return: `real_path`, `size`, `owner`, `time`, `perm` |

### Request (Single Folder)

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.CreateFolder&version=2&method=create&folder_path=/docker&name=new_folder&_sid={sid}
```

### Request (Multiple Folders)

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.CreateFolder&version=2&method=create&folder_path=["/docker","/docker"]&name=["folder1","folder2"]&_sid={sid}
```

### Response

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

Rename files or folders.

**API:** `SYNO.FileStation.Rename`  
**Version:** 2  
**Method:** `rename`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String/Array | Yes | File/folder path(s) to rename - JSON array for multiple |
| `name` | String/Array | Yes | New name(s) - JSON array for multiple |
| `additional` | String/Array | No | Additional info to return |
| `search_taskid` | String | No | Search task ID if renaming from search results |

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.Rename&version=2&method=rename&path=/docker/old_name.txt&name=new_name.txt&_sid={sid}
```

### Response

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

## SYNO.FileStation.CopyMove - Start Copy/Move

Start a copy or move operation (asynchronous for large operations).

**API:** `SYNO.FileStation.CopyMove`  
**Version:** 3  
**Method:** `start`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String/Array | Yes | Source file/folder path(s) - JSON array for multiple |
| `dest_folder_path` | String | Yes | Destination folder path |
| `overwrite` | Boolean | No | Overwrite existing files (default: false) |
| `remove_src` | Boolean | No | Remove source after copy (move operation) (default: false) |
| `accurate_progress` | Boolean | No | Calculate accurate progress (slower) (default: false) |
| `search_taskid` | String | No | Search task ID if copying from search results |

### Request (Copy)

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.CopyMove&version=3&method=start&path=/docker/file.txt&dest_folder_path=/backup&overwrite=true&_sid={sid}
```

### Request (Move)

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.CopyMove&version=3&method=start&path=/docker/file.txt&dest_folder_path=/archive&remove_src=true&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_CopyMove_12345"
  }
}
```

---

## SYNO.FileStation.CopyMove - Get Status

Check the status of a copy/move operation.

**API:** `SYNO.FileStation.CopyMove`  
**Version:** 3  
**Method:** `status`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `taskid` | String | Yes | Task ID from start operation |

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.CopyMove&version=3&method=status&taskid=FileStation_CopyMove_12345&_sid={sid}
```

### Response

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

## SYNO.FileStation.CopyMove - Stop

Stop a running copy/move operation.

**API:** `SYNO.FileStation.CopyMove`  
**Version:** 3  
**Method:** `stop`

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.CopyMove&version=3&method=stop&taskid=FileStation_CopyMove_12345&_sid={sid}
```

### Response

```json
{
  "success": true
}
```

---

## SYNO.FileStation.Delete - Start Delete

Start a delete operation (asynchronous for large operations).

**API:** `SYNO.FileStation.Delete`  
**Version:** 2  
**Method:** `start`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String/Array | Yes | File/folder path(s) to delete - JSON array for multiple |
| `accurate_progress` | Boolean | No | Calculate accurate progress (default: false) |
| `recursive` | Boolean | No | Delete folders recursively (default: true) |
| `search_taskid` | String | No | Search task ID if deleting from search results |

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.Delete&version=2&method=start&path=["/docker/temp1.txt","/docker/temp2.txt"]&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_Delete_12345"
  }
}
```

---

## SYNO.FileStation.Delete - Get Status

Check the status of a delete operation.

**API:** `SYNO.FileStation.Delete`  
**Version:** 2  
**Method:** `status`

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.Delete&version=2&method=status&taskid=FileStation_Delete_12345&_sid={sid}
```

### Response

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

## SYNO.FileStation.Delete - Stop

Stop a running delete operation.

**API:** `SYNO.FileStation.Delete`  
**Version:** 2  
**Method:** `stop`

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.Delete&version=2&method=stop&taskid=FileStation_Delete_12345&_sid={sid}
```

### Response

```json
{
  "success": true
}
```

