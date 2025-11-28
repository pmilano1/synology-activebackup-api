# AudioStation - Remote Players

**Category:** Media Management

[← Back to AudioStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.AudioStation.RemotePlayer

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.AudioStation.RemotePlayer`
- `version` (required): `1`
- `method` (required): `list`
- `type` (required): Player type (`all`, `airplay`, `chromecast`)
- `additional` (optional): Additional fields (`subplayer_list`)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "players": [
      {
        "id": "player_123",
        "name": "Living Room Speaker",
        "type": "airplay",
        "connected": true,
        "playing": false
      }
    ]
  }
}
```

---

#### Method: `getplaylist`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.AudioStation.RemotePlayer`
- `version` (required): `1`
- `method` (required): `getplaylist`
- `id` (required): Player ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "playlist": [
      {
        "id": "song_456",
        "title": "Song Title",
        "artist": "Artist Name"
      }
    ]
  }
}
```

---

#### Method: `control` (play)

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.AudioStation.RemotePlayer`
- `version` (required): `1`
- `method` (required): `control`
- `id` (required): Player ID
- `action` (required): `play`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `control` (stop)

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.AudioStation.RemotePlayer`
- `version` (required): `1`
- `method` (required): `control`
- `id` (required): Player ID
- `action` (required): `stop`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `control` (next)

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.AudioStation.RemotePlayer`
- `version` (required): `1`
- `method` (required): `control`
- `id` (required): Player ID
- `action` (required): `next`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `control` (prev)

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.AudioStation.RemotePlayer`
- `version` (required): `1`
- `method` (required): `control`
- `id` (required): Player ID
- `action` (required): `prev`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

**Notes:**
- Player ID must be obtained from `list` method first
- Supported actions: `play`, `stop`, `pause`, `next`, `prev`
- Requires compatible AirPlay or Chromecast devices

