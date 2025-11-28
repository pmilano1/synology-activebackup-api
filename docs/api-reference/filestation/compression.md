# FileStation - Compression & Extraction

**Category:** File Management

[← Back to FileStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.FileStation.Compress

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Compress`
- `version` (required): `3`
- `method` (required): `start`
- `path` (required): File/folder path (JSON array for multiple)
- `dest_file_path` (required): Destination archive path
- `_sid` (required): Session ID
- `level` (optional): Compression level
- `mode` (optional): Compression mode
- `format` (optional): Compression format (zip, 7z, tar, etc.)
- `_password` (optional): Archive password

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_Compress_12345"
  }
}
```

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Compress`
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
- `api` (required): `SYNO.FileStation.Compress`
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

## SYNO.FileStation.Extract

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Extract`
- `version` (required): `2`
- `method` (required): `start`
- `file_path` (required): Archive file path
- `dest_folder_path` (required): Destination folder
- `_sid` (required): Session ID
- `overwrite` (optional): Overwrite existing files
- `keep_dir` (optional): Keep directory structure
- `create_subfolder` (optional): Create subfolder for extracted files
- `codepage` (optional): Codepage for extraction
- `password` (optional): Archive password
- `item_id` (optional): Item ID for extraction

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "FileStation_Extract_12345"
  }
}
```

---

#### Method: `status`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.FileStation.Extract`
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
    "progress": 65.0,
    "total": 100,
    "num_processed": 65
  }
}
```

---

#### Method: `stop`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.FileStation.Extract`
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

