# FileStation - Upload & Download APIs

[← Back to FileStation](README.md)

---

## SYNO.FileStation.Upload

Upload files to the NAS.

**API:** `SYNO.FileStation.Upload`  
**Version:** 2  
**Method:** `upload`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String | Yes | Destination folder path |
| `create_parents` | Boolean | No | Create parent folders if they don't exist (default: true) |
| `overwrite` | Boolean | No | Overwrite existing files (default: false) |
| `mtime` | Integer | No | Modified time (Unix timestamp) |
| `crtime` | Integer | No | Create time (Unix timestamp) |
| `atime` | Integer | No | Access time (Unix timestamp) |
| `file` | File | Yes | File data (multipart/form-data) |

### Request (Single File)

```bash
curl -X POST "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -F "api=SYNO.FileStation.Upload" \
  -F "version=2" \
  -F "method=upload" \
  -F "path=/docker" \
  -F "create_parents=true" \
  -F "overwrite=true" \
  -F "file=@/path/to/local/document.pdf" \
  -F "_sid=YOUR_SESSION_ID"
```

### Request (Multiple Files)

```bash
curl -X POST "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -F "api=SYNO.FileStation.Upload" \
  -F "version=2" \
  -F "method=upload" \
  -F "path=/docker/uploads" \
  -F "create_parents=true" \
  -F "file=@/path/to/file1.txt" \
  -F "file=@/path/to/file2.txt" \
  -F "file=@/path/to/file3.txt" \
  -F "_sid=YOUR_SESSION_ID"
```

### Response

```json
{
  "success": true
}
```

### Python Example

```python
import requests

url = "http://YOUR_NAS_IP:5000/webapi/entry.cgi"
files = {
    'file': open('/path/to/local/file.txt', 'rb')
}
data = {
    'api': 'SYNO.FileStation.Upload',
    'version': '2',
    'method': 'upload',
    'path': '/docker',
    'create_parents': 'true',
    'overwrite': 'true',
    '_sid': 'YOUR_SESSION_ID'
}

response = requests.post(url, files=files, data=data)
print(response.json())
```

---

## SYNO.FileStation.Download

Download files from the NAS.

**API:** `SYNO.FileStation.Download`  
**Version:** 2  
**Method:** `download`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String/Array | Yes | File path(s) to download - JSON array for multiple (creates zip) |
| `mode` | String | No | Download mode: `open` (view in browser) or `download` (force download) |

### Request (Single File)

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi?api=SYNO.FileStation.Download&version=2&method=download&path=/docker/README.md&mode=download&_sid=YOUR_SESSION_ID" \
  --output README.md
```

### Request (Multiple Files - Creates ZIP)

```bash
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -G \
  --data-urlencode 'api=SYNO.FileStation.Download' \
  --data-urlencode 'version=2' \
  --data-urlencode 'method=download' \
  --data-urlencode 'path=["/docker/file1.txt","/docker/file2.txt"]' \
  --data-urlencode 'mode=download' \
  --data-urlencode "_sid=YOUR_SESSION_ID" \
  --output files.zip
```

### Response

Binary file data (or ZIP archive for multiple files)

### Python Example

```python
import requests

url = "http://YOUR_NAS_IP:5000/webapi/entry.cgi"
params = {
    'api': 'SYNO.FileStation.Download',
    'version': '2',
    'method': 'download',
    'path': '/docker/README.md',
    'mode': 'download',
    '_sid': 'YOUR_SESSION_ID'
}

response = requests.get(url, params=params, stream=True)
with open('README.md', 'wb') as f:
    for chunk in response.iter_content(chunk_size=8192):
        f.write(chunk)
```

---

## SYNO.FileStation.CheckPermission

Check write permissions before uploading.

**API:** `SYNO.FileStation.CheckPermission`  
**Version:** 3  
**Method:** `write`

### Request Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `path` | String | Yes | Destination folder path |
| `filename` | String | Yes | Filename to check |
| `overwrite` | Boolean | No | Check if overwrite is allowed (default: false) |
| `create_only` | Boolean | No | Check if file must not exist (default: false) |

### Request

```http
GET /webapi/entry.cgi?api=SYNO.FileStation.CheckPermission&version=3&method=write&path=/docker&filename=test.txt&overwrite=true&_sid={sid}
```

### Response (Permission Granted)

```json
{
  "success": true,
  "data": {
    "result": true
  }
}
```

### Response (Permission Denied)

```json
{
  "success": true,
  "data": {
    "result": false
  }
}
```

---

## Upload/Download Examples

### Upload with Progress Tracking (Python)

```python
import requests
from tqdm import tqdm

def upload_with_progress(file_path, dest_path, sid):
    url = "http://YOUR_NAS_IP:5000/webapi/entry.cgi"
    
    file_size = os.path.getsize(file_path)
    
    with open(file_path, 'rb') as f:
        files = {'file': f}
        data = {
            'api': 'SYNO.FileStation.Upload',
            'version': '2',
            'method': 'upload',
            'path': dest_path,
            'create_parents': 'true',
            'overwrite': 'true',
            '_sid': sid
        }
        
        with tqdm(total=file_size, unit='B', unit_scale=True) as pbar:
            response = requests.post(url, files=files, data=data)
            pbar.update(file_size)
    
    return response.json()
```

### Download with Progress Tracking (Python)

```python
import requests
from tqdm import tqdm

def download_with_progress(remote_path, local_path, sid):
    url = "http://YOUR_NAS_IP:5000/webapi/entry.cgi"
    params = {
        'api': 'SYNO.FileStation.Download',
        'version': '2',
        'method': 'download',
        'path': remote_path,
        'mode': 'download',
        '_sid': sid
    }
    
    response = requests.get(url, params=params, stream=True)
    total_size = int(response.headers.get('content-length', 0))
    
    with open(local_path, 'wb') as f:
        with tqdm(total=total_size, unit='B', unit_scale=True) as pbar:
            for chunk in response.iter_content(chunk_size=8192):
                f.write(chunk)
                pbar.update(len(chunk))
```

### Batch Upload Multiple Files

```bash
#!/bin/bash
SID="YOUR_SESSION_ID"
DEST_PATH="/docker/uploads"

for file in /path/to/files/*; do
    echo "Uploading $file..."
    curl -X POST "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
      -F "api=SYNO.FileStation.Upload" \
      -F "version=2" \
      -F "method=upload" \
      -F "path=$DEST_PATH" \
      -F "create_parents=true" \
      -F "overwrite=true" \
      -F "file=@$file" \
      -F "_sid=$SID"
done
```

### Download Entire Folder as ZIP

```bash
# Get list of files in folder first
FILES=$(curl -s "http://YOUR_NAS_IP:5000/webapi/entry.cgi?api=SYNO.FileStation.List&version=2&method=list&folder_path=/docker&_sid=YOUR_SESSION_ID" | jq -r '.data.files[].path')

# Convert to JSON array
FILES_JSON=$(echo "$FILES" | jq -R . | jq -s .)

# Download as ZIP
curl "http://YOUR_NAS_IP:5000/webapi/entry.cgi" \
  -G \
  --data-urlencode "api=SYNO.FileStation.Download" \
  --data-urlencode "version=2" \
  --data-urlencode "method=download" \
  --data-urlencode "path=$FILES_JSON" \
  --data-urlencode "_sid=YOUR_SESSION_ID" \
  --output folder_backup.zip
```

