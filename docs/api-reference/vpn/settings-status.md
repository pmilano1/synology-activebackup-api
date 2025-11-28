# VPN Server - Settings & Status

**Category:** Network Services

[← Back to VPN Server](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.VPNCenter.Server.Status

#### Method: `status_load`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.VPNCenter.Server.Status`
- `version` (required): `1`
- `method` (required): `status_load`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "pptp_enabled": true,
    "openvpn_enabled": true,
    "l2tp_enabled": false,
    "pptp_port": 1723,
    "openvpn_port": 1194
  }
}
```

---

## SYNO.VPNCenter.Server.Connection

#### Method: `enum`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.VPNCenter.Server.Connection`
- `version` (required): `1`
- `method` (required): `enum`
- `sort` (optional): Sort field (default: `login_time`)
- `dir` (optional): Sort direction (`ASC`, `DESC`, default: `DESC`)
- `start` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 100)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "connections": [
      {
        "id": "conn_123",
        "username": "john",
        "protocol": "openvpn",
        "ip_address": "10.8.0.2",
        "login_time": 1732752000,
        "bytes_sent": 1048576,
        "bytes_received": 2097152
      }
    ],
    "total": 1
  }
}
```

---

## SYNO.VPNCenter.Server.Log

#### Method: `load`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.VPNCenter.Server.Log`
- `version` (required): `1`
- `method` (required): `load`
- `start` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 50)
- `prtltype` (optional): Protocol type (0=all, 1=PPTP, 2=OpenVPN, 3=L2TP, default: 0)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "logs": [
      {
        "time": 1732752000,
        "user": "john",
        "protocol": "openvpn",
        "event": "connected",
        "ip_address": "192.168.1.100"
      }
    ],
    "total": 1
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `time` | integer | Event timestamp (Unix time) |
| `user` | string | Username |
| `protocol` | string | VPN protocol (pptp, openvpn, l2tp) |
| `event` | string | Event type (connected, disconnected, failed) |
| `ip_address` | string | Client IP address |

**Notes:**
- Logs are sorted by time (newest first)
- Protocol type filter: 0=all, 1=PPTP, 2=OpenVPN, 3=L2TP

