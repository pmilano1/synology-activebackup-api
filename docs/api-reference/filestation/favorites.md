# FileStation - Favorites

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.Favorite

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Favorite`
- `version` (required): `2`
- `method` (required): `list`
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results
- `sort_by` (optional): Sort field
- `status_filter` (optional): Filter by status
- `additional` (optional): Additional fields

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 5,
    "offset": 0,
    "favorites": [
      {
        "path": "/docker",
        "name": "Docker Files",
        "status": "valid"
      }
    ]
  }
}
```

---

#### Method: `add`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Favorite`
- `version` (required): `2`
- `method` (required): `add`
- `path` (required): File/folder path
- `_sid` (required): Session ID
- `name` (optional): Favorite name
- `index` (optional): Position index

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
- `api` (required): `SYNO.FileStation.Favorite`
- `version` (required): `2`
- `method` (required): `delete`
- `path` (required): Favorite path
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `clear_broken`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Favorite`
- `version` (required): `2`
- `method` (required): `clear_broken`
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
- `api` (required): `SYNO.FileStation.Favorite`
- `version` (required): `2`
- `method` (required): `edit`
- `path` (required): Favorite path
- `name` (required): New name
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `replace_all`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Favorite`
- `version` (required): `2`
- `method` (required): `replace_all`
- `path` (required): Path or paths (JSON array)
- `name` (required): Name or names (JSON array)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

