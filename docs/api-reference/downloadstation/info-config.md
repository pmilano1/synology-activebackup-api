# DownloadStation - Info & Config

**Category:** Download Management

[← Back to DownloadStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.DownloadStation.Info

#### Method: `getinfo`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Info`
- `version` (required): `2`
- `method` (required): `getinfo`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "is_manager": true,
    "version": "3.8.16-3566",
    "version_string": "3.8.16-3566"
  }
}
```

---

#### Method: `getconfig`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Info`
- `version` (required): `2`
- `method` (required): `getconfig`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "bt_max_download": 0,
    "bt_max_upload": 0,
    "emule_max_download": 0,
    "emule_max_upload": 0,
    "nzb_max_download": 0,
    "http_max_download": 0,
    "ftp_max_download": 0,
    "emule_enabled": false,
    "unzip_service_enabled": true,
    "default_destination": "/downloads",
    "emule_default_destination": "/emule"
  }
}
```

---

#### Method: `setconfig`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Info`
- `version` (required): `2`
- `method` (required): `setconfig`
- `_sid` (required): Session ID
- `bt_max_download` (optional): Max BT download speed (KB/s, 0 = unlimited)
- `bt_max_upload` (optional): Max BT upload speed (KB/s, 0 = unlimited)
- `emule_max_download` (optional): Max eMule download speed (KB/s)
- `emule_max_upload` (optional): Max eMule upload speed (KB/s)
- `nzb_max_download` (optional): Max NZB download speed (KB/s)
- `http_max_download` (optional): Max HTTP download speed (KB/s)
- `ftp_max_download` (optional): Max FTP download speed (KB/s)
- `emule_enabled` (optional): Enable eMule
- `unzip_service_enabled` (optional): Enable auto-unzip
- `default_destination` (optional): Default download destination
- `emule_default_destination` (optional): eMule download destination

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.DownloadStation.Schedule

#### Method: `getconfig`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Schedule`
- `version` (required): `1`
- `method` (required): `getconfig`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "enabled": false,
    "emule_enabled": false
  }
}
```

---

#### Method: `setconfig`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.DownloadStation.Schedule`
- `version` (required): `1`
- `method` (required): `setconfig`
- `enabled` (required): Enable schedule
- `emule_enabled` (required): Enable eMule schedule
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

