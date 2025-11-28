# FileStation - Info & Listing APIs

[← Back to FileStation](README.md)

---

## SYNO.FileStation.Info

Get FileStation information and supported features.

**API:** `SYNO.FileStation.Info`  
**Version:** 2  
**Method:** `get`

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.Info&version=2&method=get&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "is_manager": true,
    "support_virtual_protocol": ["cifs", "nfs"],
    "support_sharing": true,
    "hostname": "MyNAS",
    "enable_list_usergrp": true,
    "items": [
      {
        "path": "/volume1/homes/admin",
        "name": "home"
      }
    ]
  }
}
```

---

## SYNO.FileStation.List - List Shares

List all shared folders accessible to the current user.

**API:** `SYNO.FileStation.List`  
**Version:** 2  
**Method:** `list_share`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `offset` | Integer | No | Starting index (default: 0) |
| `limit` | Integer | No | Max results (default: 0 = all) |
| `sort_by` | String | No | Sort field: `name`, `user`, `group`, `mtime`, `atime`, `ctime`, `crtime`, `posix` |
| `sort_direction` | String | No | `asc` or `desc` (default: `asc`) |
| `onlywritable` | Boolean | No | Only show writable shares |
| `additional` | String/Array | No | Additional info: `real_path`, `owner`, `time`, `perm`, `mount_point_type`, `volume_status` |

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.List&version=2&method=list_share&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "total": 3,
    "offset": 0,
    "shares": [
      {
        "path": "/docker",
        "name": "docker",
        "isdir": true,
        "additional": {
          "real_path": "/volume1/docker",
          "owner": {
            "user": "admin",
            "group": "administrators",
            "uid": 1024,
            "gid": 100
          },
          "time": {
            "atime": 1732752000,
            "mtime": 1732752000,
            "ctime": 1732752000,
            "crtime": 1732752000
          },
          "perm": {
            "posix": 755,
            "is_acl_mode": false,
            "acl": {
              "append": false,
              "del": false,
              "exec": true,
              "read": true,
              "write": false
            }
          }
        }
      }
    ]
  }
}
```

---

## SYNO.FileStation.List - List Files

List files and folders in a directory.

**API:** `SYNO.FileStation.List`  
**Version:** 2  
**Method:** `list`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `folder_path` | String | Yes | Path to folder |
| `offset` | Integer | No | Starting index (default: 0) |
| `limit` | Integer | No | Max results (default: 0 = all) |
| `sort_by` | String | No | Sort field: `name`, `size`, `user`, `group`, `mtime`, `atime`, `ctime`, `crtime`, `posix`, `type` |
| `sort_direction` | String | No | `asc` or `desc` (default: `asc`) |
| `pattern` | String | No | File name pattern (supports wildcards) |
| `filetype` | String | No | Filter by type: `file`, `dir`, `all` (default: `all`) |
| `goto_path` | String | No | Jump to specific file path |
| `additional` | String/Array | No | Additional info: `real_path`, `size`, `owner`, `time`, `perm`, `mount_point_type`, `type` |

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.List&version=2&method=list&folder_path=/docker&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "total": 15,
    "offset": 0,
    "files": [
      {
        "path": "/docker/compose",
        "name": "compose",
        "isdir": true,
        "additional": {
          "size": 4096,
          "time": {
            "atime": 1732752000,
            "mtime": 1732752000,
            "ctime": 1732752000,
            "crtime": 1732752000
          }
        }
      },
      {
        "path": "/docker/README.md",
        "name": "README.md",
        "isdir": false,
        "additional": {
          "size": 2048,
          "type": "text/markdown"
        }
      }
    ]
  }
}
```

---

## SYNO.FileStation.List - Get File Info

Get detailed information about specific files or folders.

**API:** `SYNO.FileStation.List`  
**Version:** 2  
**Method:** `getinfo`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String/Array | Yes | File/folder path(s) - JSON array for multiple |
| `additional` | String/Array | No | Additional info: `real_path`, `size`, `owner`, `time`, `perm`, `mount_point_type`, `type` |

### Request (Single File)

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.List&version=2&method=getinfo&path=/docker/README.md&additional=size,time&_sid={sid}
```

### Request (Multiple Files)

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.List&version=2&method=getinfo&path=["/docker/file1.txt","/docker/file2.txt"]&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "files": [
      {
        "path": "/docker/README.md",
        "name": "README.md",
        "isdir": false,
        "additional": {
          "size": 2048,
          "time": {
            "atime": 1732752000,
            "mtime": 1732752000,
            "ctime": 1732752000,
            "crtime": 1732752000
          }
        }
      }
    ]
  }
}
```

