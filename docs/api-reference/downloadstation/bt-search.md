# DownloadStation - BitTorrent Search

**Category:** Download Management

[← Back to DownloadStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.DownloadStation.BTSearch

#### Method: `start`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.BTSearch`
- `version` (required): `1`
- `method` (required): `start`
- `keyword` (required): Search keyword
- `_sid` (required): Session ID
- `module` (optional): Search module (default: `all`)

**Response:**
```json
{
  "success": true,
  "data": {
    "taskid": "btsearch_1"
  }
}
```

---

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.BTSearch`
- `version` (required): `1`
- `method` (required): `list`
- `taskid` (required): Search task ID
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results
- `sort_by` (optional): Sort field: `title`, `size`, `date`, `peers`, `seeds`, `leechs`
- `sort_direction` (optional): `asc` or `desc`
- `filter_category` (optional): Filter by category
- `filter_title` (optional): Filter by title

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 50,
    "offset": 0,
    "finished": true,
    "items": [
      {
        "title": "Ubuntu 22.04 LTS Desktop",
        "download": "magnet:?xt=urn:btih:...",
        "size": 3774873600,
        "date": "2023-04-21",
        "peers": 150,
        "seeds": 500,
        "leechs": 50,
        "category": "Software"
      }
    ]
  }
}
```

---

#### Method: `getCategory`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.BTSearch`
- `version` (required): `1`
- `method` (required): `getCategory`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "categories": [
      "All",
      "Movie",
      "TV",
      "Music",
      "Software",
      "Game",
      "Book",
      "Other"
    ]
  }
}
```

---

#### Method: `getModule`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.BTSearch`
- `version` (required): `1`
- `method` (required): `getModule`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "modules": [
      {
        "name": "all",
        "displayname": "All"
      },
      {
        "name": "piratebay",
        "displayname": "The Pirate Bay"
      }
    ]
  }
}
```

---

#### Method: `clean`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.BTSearch`
- `version` (required): `1`
- `method` (required): `clean`
- `taskid` (required): Task ID (comma-separated for multiple)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

