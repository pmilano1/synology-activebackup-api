# FileStation - Search APIs

[← Back to FileStation](README.md)

---

## SYNO.FileStation.Search - Start Search

Start a file search task.

**API:** `SYNO.FileStation.Search`  
**Version:** 2  
**Method:** `start`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `folder_path` | String | Yes | Starting folder path for search |
| `recursive` | Boolean | No | Search recursively (default: true) |
| `pattern` | String | No | File name pattern (supports wildcards: `*`, `?`) |
| `extension` | String | No | File extension filter (e.g., `jpg,png,pdf`) |
| `filetype` | String | No | Filter by type: `file`, `dir`, `all` (default: `all`) |
| `size_from` | Integer | No | Minimum file size in bytes |
| `size_to` | Integer | No | Maximum file size in bytes |
| `mtime_from` | Integer | No | Modified after timestamp (Unix epoch) |
| `mtime_to` | Integer | No | Modified before timestamp (Unix epoch) |
| `crtime_from` | Integer | No | Created after timestamp (Unix epoch) |
| `crtime_to` | Integer | No | Created before timestamp (Unix epoch) |
| `atime_from` | Integer | No | Accessed after timestamp (Unix epoch) |
| `atime_to` | Integer | No | Accessed before timestamp (Unix epoch) |
| `owner` | String | No | Filter by owner username |
| `group` | String | No | Filter by group name |

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.Search&version=2&method=start&folder_path=/docker&pattern=*.md&recursive=true&_sid={sid}
```

### Response

```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_12345"
  }
}
```

---

## SYNO.FileStation.Search - List Results

Get search results from a running or completed search task.

**API:** `SYNO.FileStation.Search`  
**Version:** 2  
**Method:** `list`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `taskid` | String | Yes | Task ID from start search |
| `offset` | Integer | No | Starting index (default: 0) |
| `limit` | Integer | No | Max results (default: 0 = all) |
| `sort_by` | String | No | Sort field: `name`, `size`, `user`, `group`, `mtime`, `atime`, `ctime`, `crtime`, `posix`, `type` |
| `sort_direction` | String | No | `asc` or `desc` (default: `asc`) |
| `pattern` | String | No | Additional pattern filter |
| `filetype` | String | No | Filter by type: `file`, `dir`, `all` |
| `additional` | String/Array | No | Additional info: `real_path`, `size`, `owner`, `time`, `perm`, `mount_point_type`, `type` |

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.Search&version=2&method=list&taskid=FileStation_12345&_sid={sid}
```

### Response

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
      },
      {
        "path": "/docker/services/CHANGELOG.md",
        "name": "CHANGELOG.md",
        "isdir": false,
        "additional": {
          "size": 1024,
          "time": {
            "mtime": 1732751000
          }
        }
      }
    ]
  }
}
```

**Response Fields:**
- `finished` - `true` if search is complete, `false` if still running
- `total` - Total number of results found so far
- `files` - Array of matching files

---

## SYNO.FileStation.Search - Get Status

Check the status of a search task without retrieving results.

**API:** `SYNO.FileStation.Search`  
**Version:** 2  
**Method:** `status`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `taskid` | String | Yes | Task ID from start search |

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.Search&version=2&method=status&taskid=FileStation_12345&_sid={sid}
```

### Response

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

**Response Fields:**
- `finished` - `true` if search is complete
- `total` - Total results found so far
- `num_found` - Number of results found

---

## SYNO.FileStation.Search - Stop Search

Stop a running search task.

**API:** `SYNO.FileStation.Search`  
**Version:** 2  
**Method:** `stop`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `taskid` | String | Yes | Task ID to stop |

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.Search&version=2&method=stop&taskid=FileStation_12345&_sid={sid}
```

### Response

```json
{
  "success": true
}
```

---

## SYNO.FileStation.Search - Clean Search

Clean up completed search tasks to free resources.

**API:** `SYNO.FileStation.Search`  
**Version:** 2  
**Method:** `clean`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `taskid` | String | Yes | Task ID to clean (use `all` to clean all completed tasks) |

### Request

```http
POST /webapi/entry.cgi
Content-Type: application/x-www-form-urlencoded

api=SYNO.FileStation.Search&version=2&method=clean&taskid=FileStation_12345&_sid={sid}
```

### Response

```json
{
  "success": true
}
```

---

## Search Examples

### Search for PDF Files Modified in Last 7 Days

```bash
# Calculate timestamp for 7 days ago
SEVEN_DAYS_AGO=$(date -d '7 days ago' +%s)

curl -X POST "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.Search" \
  -d "version=2" \
  -d "method=start" \
  -d "folder_path=/home" \
  -d "extension=pdf" \
  -d "mtime_from=$SEVEN_DAYS_AGO" \
  -d "recursive=true" \
  -d "_sid=YOUR_SESSION_ID"
```

### Search for Large Files (>100MB)

```bash
curl -X POST "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.Search" \
  -d "version=2" \
  -d "method=start" \
  -d "folder_path=/docker" \
  -d "size_from=104857600" \
  -d "filetype=file" \
  -d "_sid=YOUR_SESSION_ID"
```

### Search for Files by Owner

```bash
curl -X POST "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -d "api=SYNO.FileStation.Search" \
  -d "version=2" \
  -d "method=start" \
  -d "folder_path=/homes" \
  -d "owner=admin" \
  -d "recursive=true" \
  -d "_sid=YOUR_SESSION_ID"
```

