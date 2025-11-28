# FileStation - Info & Listing

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.Info

#### Method: `get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Info`
- `version` (required): `2`
- `method` (required): `get`
- `_sid` (required): Session ID

**Response:**
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

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `is_manager` | boolean | User has manager privileges |
| `support_virtual_protocol` | array | Supported virtual protocols |
| `support_sharing` | boolean | Sharing feature supported |
| `hostname` | string | NAS hostname |
| `enable_list_usergrp` | boolean | Can list users/groups |

---

## SYNO.FileStation.List

#### Method: `list_share`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.List`
- `version` (required): `2`
- `method` (required): `list_share`
- `_sid` (required): Session ID
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 0 = all)
- `sort_by` (optional): Sort field: `name`, `user`, `group`, `mtime`, `atime`, `ctime`, `crtime`, `posix`
- `sort_direction` (optional): `asc` or `desc`
- `onlywritable` (optional): Only writable shares
- `additional` (optional): Additional fields: `real_path`, `owner`, `time`, `perm`, `mount_point_type`, `volume_status`

**Response:**
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

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `total` | integer | Total number of shares |
| `offset` | integer | Current offset |
| `shares` | array | Array of share objects |
| `path` | string | Share path |
| `name` | string | Share name |
| `isdir` | boolean | Is directory |

---

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.List`
- `version` (required): `2`
- `method` (required): `list`
- `folder_path` (required): Folder path
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results
- `sort_by` (optional): Sort field: `name`, `size`, `user`, `group`, `mtime`, `atime`, `ctime`, `crtime`, `posix`, `type`
- `sort_direction` (optional): `asc` or `desc`
- `pattern` (optional): File name pattern
- `filetype` (optional): `file`, `dir`, `all`
- `goto_path` (optional): Jump to specific path
- `additional` (optional): Additional fields: `real_path`, `size`, `owner`, `time`, `perm`, `mount_point_type`, `type`

**Response:**
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
      }
    ]
  }
}
```

---

#### Method: `getinfo`

**HTTP Method:** GET/POST

**Parameters:**
- `api` (required): `SYNO.FileStation.List`
- `version` (required): `2`
- `method` (required): `getinfo`
- `path` (required): File/folder path (JSON array for multiple)
- `_sid` (required): Session ID
- `additional` (optional): Additional fields

**Response:**
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

