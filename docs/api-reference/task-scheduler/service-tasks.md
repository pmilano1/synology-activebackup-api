# Task Scheduler - Service Tasks

**Category:** Automation

[← Back to Task Scheduler](README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## SYNO.Core.TaskScheduler.Service

#### Method: `Create`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler.Service`
- `version` (required): `1`
- `method` (required): `Create`
- `task_name` (required): Task name
- `service_name` (required): Service name
- `action` (required): Service action (`start`, `stop`, `restart`)
- `schedule` (required): Schedule configuration (JSON object)
- `enabled` (optional): Enable task (default: true)
- `_sid` (required): Session ID

**Response:**
```json
{
  "success": true,
  "data": {
    "task_id": 6
  }
}
```

**Common Service Names:**
- `sshd` - SSH service
- `nmbd` - Samba NetBIOS service
- `smbd` - Samba file sharing service
- `afpd` - AFP file sharing service
- `ftpd` - FTP service
- `nfsd` - NFS service
- `snmpd` - SNMP service

---

#### Method: `Modify`

**HTTP Method:** POST

**Parameters:**
- `api` (required): `SYNO.Core.TaskScheduler.Service`
- `version` (required): `1`
- `method` (required): `Modify`
- `task_id` (required): Task ID
- `task_name` (optional): New task name
- `service_name` (optional): New service name
- `action` (optional): New service action
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
- Service tasks control DSM system services
- Useful for scheduled service restarts
- Actions: `start`, `stop`, `restart`
- Requires administrator privileges

---

## Example Service Tasks

**Restart SSH Daily:**
```json
{
  "task_name": "Daily SSH Restart",
  "service_name": "sshd",
  "action": "restart",
  "schedule": {
    "date_type": 0,
    "hour": 3,
    "minute": 0
  }
}
```

**Stop FTP on Weekends:**
```json
{
  "task_name": "Weekend FTP Stop",
  "service_name": "ftpd",
  "action": "stop",
  "schedule": {
    "date_type": 1,
    "hour": 18,
    "minute": 0,
    "week_day": "5"
  }
}
```

**Start FTP on Weekdays:**
```json
{
  "task_name": "Weekday FTP Start",
  "service_name": "ftpd",
  "action": "start",
  "schedule": {
    "date_type": 1,
    "hour": 8,
    "minute": 0,
    "week_day": "1"
  }
}
```

**Notes:**
- Service control tasks are useful for security and resource management
- Stopping services reduces attack surface
- Restarting services can resolve memory leaks
- Coordinate start/stop tasks to avoid conflicts

