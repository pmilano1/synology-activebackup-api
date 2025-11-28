# DownloadStation - RSS

**Category:** Download Management

[← Back to DownloadStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.DownloadStation.RSS.Site

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.RSS.Site`
- `version` (required): `1`
- `method` (required): `list`
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 2,
    "offset": 0,
    "sites": [
      {
        "id": "rss_1",
        "title": "Ubuntu Releases",
        "url": "https://releases.ubuntu.com/rss",
        "is_updating": false,
        "last_update": 1732752000
      }
    ]
  }
}
```

---

#### Method: `refresh`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.RSS.Site`
- `version` (required): `1`
- `method` (required): `refresh`
- `id` (required): RSS site ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.DownloadStation.RSS.Feed

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.RSS.Feed`
- `version` (required): `1`
- `method` (required): `list`
- `id` (required): RSS site ID
- `_sid` (required): Session ID
- `offset` (optional): Starting index
- `limit` (optional): Max results

**Response:**
```json
{
  "success": true,
  "data": {
    "total": 10,
    "offset": 0,
    "feeds": [
      {
        "id": "feed_1",
        "title": "Ubuntu 22.04 LTS",
        "url": "https://releases.ubuntu.com/22.04/ubuntu-22.04-desktop-amd64.iso.torrent",
        "download_uri": "https://releases.ubuntu.com/22.04/ubuntu-22.04-desktop-amd64.iso.torrent",
        "publish_date": 1732752000
      }
    ]
  }
}
```

