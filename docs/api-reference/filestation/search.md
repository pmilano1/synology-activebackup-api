# FileStation - Search

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.Search

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Search`
- `version` (required): `2`
- `method` (required): `start`
- `folder_path` (required): Starting folder path
- `_sid` (required): Session ID
- `recursive` (optional): Search recursively (default: true)
- `pattern` (optional): File name pattern (wildcards: `*`, `?`)
- `extension` (optional): File extensions (comma-separated)
- `filetype` (optional): `file`, `dir`, `all`
- `size_from` (optional): Minimum file size (bytes)
- `size_to` (optional): Maximum file size (bytes)
- `mtime_from` (optional): Modified after (Unix timestamp)
- `mtime_to` (optional): Modified before (Unix timestamp)
- `crtime_from` (optional): Created after (Unix timestamp)
- `crtime_to` (optional): Created before (Unix timestamp)
- `atime_from` (optional): Accessed after (Unix timestamp)
- `atime_to` (optional): Accessed before (Unix timestamp)
- `owner` (optional): Owner username
- `group` (optional): Group name

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_12345"
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `taskid` | string | Search task ID |

---

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Search`
- `version` (required): `2`
- `method` (required): `list`
- `taskid` (required): Task ID from start
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results
- `sort_by` (optional): Sort field: `name`, `size`, `user`, `group`, `mtime`, `atime`, `ctime`, `crtime`, `posix`, `type`
- `sort_direction` (optional): `asc` or `desc`
- `pattern` (optional): Additional pattern filter
- `filetype` (optional): `file`, `dir`, `all`
- `additional` (optional): Additional fields

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 5,
    "offset": 0,
    "finished": true,
    "files": [
      {
        "path": "/docker/README.md",
        "name": "README.md",
        "isdir": false,
        "additional": {
          "size": 2048,
          "time": {
            "mtime": 1732752000
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
| `finished` | boolean | Search complete |
| `total` | integer | Total results found |
| `files` | array | Matching files |

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Search`
- `version` (required): `2`
- `method` (required): `status`
- `taskid` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "finished": false,
    "total": 3,
    "num_found": 3
  }
}
```

---

#### Method: `stop`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Search`
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

#### Method: `clean`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Search`
- `version` (required): `2`
- `method` (required): `clean`
- `taskid` (required): Task ID (use `all` for all completed tasks)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

