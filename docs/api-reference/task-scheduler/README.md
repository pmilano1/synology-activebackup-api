# Task Scheduler APIs

**Category:** Automation

[← Back to API Reference](../README.md)

---

**Endpoint:** `/webapi/entry.cgi`

---

## Overview

Task Scheduler APIs provide comprehensive task automation including script execution, service control, beep control, and recycle bin management.

---

## API Categories

| Category | Description |
|----------|-------------|
| **[Task Management](task-management.md)** | List, get, enable, disable, run, delete tasks |
| **[Script Tasks](script-tasks.md)** | Create and modify script execution tasks |
| **[Service Tasks](service-tasks.md)** | Create and modify service control tasks |

---

## Common Parameters

**Session Management:**
- `_sid` - Session ID (required for all APIs)

**Task Identification:**
- `task_id` - Task ID

**Scheduling:**
- `schedule` - Schedule configuration object

---

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Invalid parameter |
| 401 | Unknown error |
| 403 | Permission denied |
| 404 | Task not found |

---

## Notes

- Task Scheduler is built into DSM
- Tasks can run scripts, control services, manage recycle bin
- Supports various schedule types (daily, weekly, monthly, custom)
- Tasks can be enabled/disabled without deletion
- Output logging available for debugging

