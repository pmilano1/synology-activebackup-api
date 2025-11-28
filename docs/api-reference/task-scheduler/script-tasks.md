# Task Scheduler - Script Tasks

**Category:** Automation

[← Back to Task Scheduler](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.Core.TaskScheduler.Script

#### Method: `Create`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler.Script`
- `version` (required): `2`
- `method` (required): `Create`
- `task_name` (required): Task name
- `script` (required): Script content
- `schedule` (required): Schedule configuration (JSON object)
- `enabled` (optional): Enable task (default: true)
- `notify_enable` (optional): Enable notifications (default: false)
- `notify_mail` (optional): Notification email
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "task_id": 5
  }
}
```

**Schedule Configuration:**
```json
{
  "date_type": 0,
  "hour": 2,
  "minute": 0,
  "repeat_hour": 0,
  "repeat_min": 0,
  "last_work_hour": 0,
  "week_day": "0,1,2,3,4,5,6"
}
```

**Schedule Types:**
- `date_type: 0` - Daily
- `date_type: 1` - Weekly (use `week_day`)
- `date_type: 2` - Monthly (use `month_day`)
- `date_type: 3` - Run on boot
- `date_type: 4` - Repeat (use `repeat_hour`, `repeat_min`)

---

#### Method: `Modify`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler.Script`
- `version` (required): `2`
- `method` (required): `Modify`
- `task_id` (required): Task ID
- `task_name` (optional): New task name
- `script` (optional): New script content
- `schedule` (optional): New schedule configuration
- `enabled` (optional): Enable status
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true
}
```

**Notes:**
- Scripts can be bash, python, or other interpreters
- Use shebang line (e.g., `#!/bin/bash`) to specify interpreter
- Scripts run with DSM user permissions
- Output can be logged for debugging

---

## Example Script Task

**Daily Backup Script:**
```bash
#!/bin/bash
# Daily backup script
SOURCE="/volume1/important"
DEST="/volume1/backup/$(date +%Y%m%d)"
mkdir -p "$DEST"
rsync -av "$SOURCE/" "$DEST/"
echo "Backup completed: $DEST"
```

**Schedule (Daily at 2:00 AM):**
```json
{
  "date_type": 0,
  "hour": 2,
  "minute": 0
}
```

**Repeat Every 30 Minutes:**
```json
{
  "date_type": 4,
  "repeat_hour": 0,
  "repeat_min": 30,
  "last_work_hour": 23
}
```

**Weekly on Monday and Friday:**
```json
{
  "date_type": 1,
  "hour": 9,
  "minute": 0,
  "week_day": "1,5"
}
```

**Notes:**
- Week days: 0=Sunday, 1=Monday, ..., 6=Saturday
- Scripts have access to DSM environment variables
- Long-running scripts should handle interruption gracefully
- Use absolute paths in scripts

