# DownloadStation - Tasks

**Category:** Download Management

[← Back to DownloadStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.DownloadStation.Task

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `1`
- `method` (required): `list`
- `_sid` (required): Session ID
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: -1 = all)
- `additional` (optional): Additional fields (comma-separated): `detail`, `transfer`, `file`, `tracker`, `peer`

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 2,
    "offset": 0,
    "tasks": [
      {
        "id": "dbid_1",
        "type": "bt",
        "username": "admin",
        "title": "ubuntu-22.04.iso",
        "size": 3774873600,
        "status": "downloading",
        "additional": {
          "detail": {
            "destination": "/downloads",
            "uri": "magnet:?xt=urn:btih:..."
          },
          "transfer": {
            "size_downloaded": 1887436800,
            "size_uploaded": 94371840,
            "speed_download": 1048576,
            "speed_upload": 52428
          }
        }
      }
    ]
  }
}
```

---

#### Method: `getinfo`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `1`
- `method` (required): `getinfo`
- `id` (required): Task ID (comma-separated for multiple)
- `_sid` (required): Session ID
- `additional` (optional): Additional fields

**Response:**
```json
{
  "success": true,
  "data": {
    "tasks": [
      {
        "id": "dbid_1",
        "type": "bt",
        "title": "ubuntu-22.04.iso",
        "size": 3774873600,
        "status": "downloading"
      }
    ]
  }
}
```

---

#### Method: `create`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `3`
- `method` (required): `create`
- `_sid` (required): Session ID
- `uri` (optional): Download URL (HTTP, FTP, magnet, etc.)
- `file` (optional): Torrent file (multipart/form-data)
- `destination` (optional): Download destination path

**Notes:**
- Use either `uri` or `file`, not both
- Supports HTTP, HTTPS, FTP, magnet links, and torrent files

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `delete`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `1`
- `method` (required): `delete`
- `id` (required): Task ID (comma-separated for multiple)
- `_sid` (required): Session ID
- `force_complete` (optional): Force delete even if not complete

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `pause`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `1`
- `method` (required): `pause`
- `id` (required): Task ID (comma-separated for multiple)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `resume`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `1`
- `method` (required): `resume`
- `id` (required): Task ID (comma-separated for multiple)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `edit`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Task`
- `version` (required): `1`
- `method` (required): `edit`
- `id` (required): Task ID (comma-separated for multiple)
- `_sid` (required): Session ID
- `destination` (optional): New download destination

**Response:**
```json
{
  "success": true
}
```

