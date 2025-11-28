# DownloadStation - Statistics

**Category:** Download Management

[← Back to DownloadStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.DownloadStation.Statistic

#### Method: `getinfo`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Statistic`
- `version` (required): `1`
- `method` (required): `getinfo`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "speed_download": 1048576,
    "speed_upload": 52428,
    "emule_speed_download": 0,
    "emule_speed_upload": 0,
    "nzb_speed_download": 0
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `speed_download` | integer | Current download speed (bytes/s) |
| `speed_upload` | integer | Current upload speed (bytes/s) |
| `emule_speed_download` | integer | eMule download speed (bytes/s) |
| `emule_speed_upload` | integer | eMule upload speed (bytes/s) |
| `nzb_speed_download` | integer | NZB download speed (bytes/s) |

