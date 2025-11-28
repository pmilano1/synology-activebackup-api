# System Services - Universal Search

**Category:** System Management

[← Back to System Services](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.Finder.FileIndexing.Search

#### Method: `Search`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.Finder.FileIndexing.Search`
- `version` (required): `1`
- `method` (required): `Search`
- `keyword` (required): Search keyword
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 100)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "results": [
      {
        "path": "/volume1/Documents/report.pdf",
        "name": "report.pdf",
        "type": "file",
        "size": 1048576,
        "modified_time": 1732788000
      },
      {
        "path": "/volume1/Photos/vacation",
        "name": "vacation",
        "type": "folder",
        "modified_time": 1732788000
      }
    ],
    "total": 2
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `path` | string | Full file/folder path |
| `name` | string | File/folder name |
| `type` | string | Type (`file`, `folder`) |
| `size` | integer | File size (bytes, files only) |
| `modified_time` | integer | Last modified timestamp (Unix time) |

**Notes:**
- Universal Search indexes files across all shared folders
- Searches file names and metadata
- Indexing must be enabled in DSM settings
- Search results respect user permissions
- Supports wildcard searches with `*` and `?`

