# System Services - Note Station

**Category:** Productivity

[← Back to System Services](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.NoteStation.Note

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.NoteStation.Note`
- `version` (required): `1`
- `method` (required): `List`
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 100)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "notes": [
      {
        "note_id": "note_123",
        "title": "Meeting Notes",
        "content": "Discussion points...",
        "notebook_id": "notebook_1",
        "created_time": 1732788000,
        "updated_time": 1732788000,
        "tags": ["work", "meeting"]
      }
    ],
    "total": 1
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `note_id` | string | Note ID |
| `title` | string | Note title |
| `content` | string | Note content |
| `notebook_id` | string | Parent notebook ID |
| `created_time` | integer | Creation timestamp (Unix time) |
| `updated_time` | integer | Last update timestamp (Unix time) |
| `tags` | array | Note tags |

---

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.NoteStation.Note`
- `version` (required): `1`
- `method` (required): `Get`
- `note_id` (required): Note ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "note_id": "note_123",
    "title": "Meeting Notes",
    "content": "Discussion points...",
    "notebook_id": "notebook_1",
    "created_time": 1732788000,
    "updated_time": 1732788000,
    "tags": ["work", "meeting"]
  }
}
```

---

## SYNO.NoteStation.Notebook

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.NoteStation.Notebook`
- `version` (required): `1`
- `method` (required): `List`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "notebooks": [
      {
        "notebook_id": "notebook_1",
        "name": "Work",
        "note_count": 15,
        "created_time": 1732788000
      }
    ],
    "total": 1
  }
}
```

---

## SYNO.NoteStation.Tag

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.NoteStation.Tag`
- `version` (required): `1`
- `method` (required): `List`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "tags": [
      {
        "tag_name": "work",
        "note_count": 10
      },
      {
        "tag_name": "meeting",
        "note_count": 5
      }
    ],
    "total": 2
  }
}
```

**Notes:**
- Note Station package must be installed
- Notes support rich text formatting
- Tags help organize notes across notebooks
- Notes can be shared with other users

