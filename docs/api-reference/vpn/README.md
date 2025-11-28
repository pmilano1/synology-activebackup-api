# VPN Server APIs

**Category:** Network Services

[← Back to API Reference](../README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## Overview

VPN Server APIs provide access to VPN server configuration, active connections, logs, and protocol-specific settings (PPTP, OpenVPN, L2TP).

---

## API Methods

### [Settings & Status](settings-status.md)
VPN server settings, active connections, logs

### [Network & Security](network-security.md)
Network interface settings, security autoblock, permissions

### [Protocols](protocols.md)
PPTP, OpenVPN, L2TP settings and configuration export

---

## Common Parameters

**Session Management:**
- `_sid` - Session ID (required for all APIs)

**Pagination:**
- `start` - Starting index
- `limit` - Maximum results

**Sorting:**
- `sort` - Sort field
- `dir` - Sort direction (`ASC`, `DESC`)

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid parameter |
| 401 | Unknown error |
| 402 | VPN Server not enabled |
| 403 | Permission denied |

---

## Notes

- VPN Server package must be installed
- Requires administrator privileges
- OpenVPN configuration can be exported as ZIP file

