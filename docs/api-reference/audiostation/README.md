# AudioStation APIs

**Category:** Media Management

[← Back to API Reference](../README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## Overview

AudioStation APIs provide access to music library management, playlist control, and remote player management.

---

## API Methods

### [Info & Playlists](info-playlists.md)
Get AudioStation info, list playlists, list pinned songs

### [Remote Players](remote-players.md)
List remote players, control playback (play, stop, next, prev)

---

## Common Parameters

**Session Management:**
- `_sid` - Session ID (required for all APIs)

**Pagination:**
- `offset` - Starting index
- `limit` - Maximum results

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid parameter |
| 401 | Unknown error |
| 402 | AudioStation not enabled |
| 403 | Permission denied |

---

## Notes

- AudioStation package must be installed
- Remote player control requires compatible devices
- Playlist operations support library filtering

