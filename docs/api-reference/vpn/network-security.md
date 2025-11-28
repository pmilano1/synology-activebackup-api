# VPN Server - Network & Security

**Category:** Network Services

[← Back to VPN Server](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.VPNCenter.Server.NetworkInterface

#### Method: `load`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.VPNCenter.Server.NetworkInterface`
- `version` (required): `1`
- `method` (required): `load`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "interfaces": [
      {
        "name": "tun0",
        "type": "openvpn",
        "ip_address": "10.8.0.1",
        "netmask": "255.255.255.0",
        "status": "up"
      }
    ]
  }
}
```

---

## SYNO.Core.SecurityAutoBlock

#### Method: `get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.Core.SecurityAutoBlock`
- `version` (required): `1`
- `method` (required): `get`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "enabled": true,
    "login_attempt": 5,
    "expire_min": 30,
    "block_expire_min": 1440
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `enabled` | boolean | Auto-block enabled |
| `login_attempt` | integer | Failed login attempts before block |
| `expire_min` | integer | Minutes to track failed attempts |
| `block_expire_min` | integer | Minutes to block IP address |

---

## SYNO.VPNCenter.Server.Privilege

#### Method: `load`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.VPNCenter.Server.Privilege`
- `version` (required): `1`
- `method` (required): `load`
- `action` (required): `enum`
- `start` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 100)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "privileges": [
      {
        "name": "john",
        "type": "user",
        "pptp": true,
        "openvpn": true,
        "l2tp": false
      },
      {
        "name": "vpn_users",
        "type": "group",
        "pptp": true,
        "openvpn": true,
        "l2tp": true
      }
    ],
    "total": 2
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `name` | string | User or group name |
| `type` | string | Type (`user`, `group`) |
| `pptp` | boolean | PPTP access allowed |
| `openvpn` | boolean | OpenVPN access allowed |
| `l2tp` | boolean | L2TP access allowed |

**Notes:**
- Permissions can be set per user or group
- At least one protocol must be enabled for access

