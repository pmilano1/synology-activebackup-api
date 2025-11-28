# AudioStation - Info & Playlists

**Category:** Media Management

[← Back to AudioStation](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.AudioStation.Info

#### Method: `getinfo`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.AudioStation.Info`
- `version` (required): `1`
- `method` (required): `getinfo`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "is_manager": true,
    "version": "6.5.5-3374",
    "version_string": "6.5.5-3374"
  }
}
```

---

## SYNO.AudioStation.Playlist

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.AudioStation.Playlist`
- `version` (required): `1`
- `method` (required): `list`
- `library` (required): Library filter (`all`, `personal`, `shared`)
- `limit` (optional): Max results (default: 100000)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "playlists": [
      {
        "id": "playlist_123",
        "name": "My Favorites",
        "type": "normal",
        "library": "personal",
        "sharing_status": "private"
      }
    ],
    "total": 1
  }
}
```

---

## SYNO.AudioStation.Pin

#### Method: `list`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.AudioStation.Pin`
- `version` (required): `1`
- `method` (required): `list`
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "songs": [
      {
        "id": "music_456",
        "title": "Song Title",
        "artist": "Artist Name",
        "album": "Album Name"
      }
    ]
  }
}
```

**Notes:**
- Pinned songs are user-specific favorites
- Requires AudioStation 6.0 or later

