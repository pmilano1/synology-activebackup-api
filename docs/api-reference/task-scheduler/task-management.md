# Task Scheduler - Task Management

**Category:** Automation

[← Back to Task Scheduler](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.Core.TaskScheduler

#### Method: `List`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler`
- `version` (required): `2`
- `method` (required): `List`
- `sort_by` (optional): Sort field (default: `next_trigger_time`)
- `sort_direction` (optional): Sort direction (`asc`, `desc`)
- `offset` (optional): Starting index (default: 0)
- `limit` (optional): Max results (default: 100)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "tasks": [
      {
        "id": 1,
        "name": "Daily Backup",
        "type": "script",
        "enabled": true,
        "next_trigger_time": 1732788000,
        "last_run_time": 1732701600,
        "last_run_status": "success"
      }
    ],
    "total": 1
  }
}
```

**Response Fields:**

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Task ID |
| `name` | string | Task name |
| `type` | string | Task type (`script`, `service`, `beep`, `recycle_bin`) |
| `enabled` | boolean | Task enabled |
| `next_trigger_time` | integer | Next run timestamp (Unix time) |
| `last_run_time` | integer | Last run timestamp (Unix time) |
| `last_run_status` | string | Last run status (`success`, `failed`) |

---

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler`
- `version` (required): `2`
- `method` (required): `Get`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "id": 1,
    "name": "Daily Backup",
    "type": "script",
    "enabled": true,
    "schedule": {
      "date_type": 0,
      "hour": 2,
      "minute": 0
    },
    "script": "#!/bin/bash\necho 'Backup started'"
  }
}
```

---

#### Method: `SetEnable`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler`
- `version` (required): `2`
- `method` (required): `SetEnable`
- `task_id` (required): Task ID
- `enable` (required): Enable status (true/false)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

#### Method: `Run`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler`
- `version` (required): `2`
- `method` (required): `Run`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

**Notes:**
- Runs task immediately regardless of schedule
- Task must be enabled to run

---

#### Method: `Delete`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler`
- `version` (required): `2`
- `method` (required): `Delete`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

---

## SYNO.Core.TaskScheduler.Result

#### Method: `Get`

**HTTP Method:** GET

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler.Result`
- `version` (required): `1`
- `method` (required): `Get`
- `task_id` (required): Task ID
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "results": [
      {
        "time": 1732701600,
        "status": "success",
        "output": "Backup completed successfully"
      }
    ]
  }
}
```

**Notes:**
- Task results include execution output
- Output logging must be enabled in task settings
- Results are limited to recent executions

