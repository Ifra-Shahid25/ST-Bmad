# EPIC 11 - Follow-up Tasks & Notification

### Story 11.1 Tasks, Reminders, and Notifications
User Story: As a user, I want tasks and reminders with notifications so that follow-ups are not missed.
Acceptance:
- Create/assign tasks with due dates/status; escalations/reminders configurable.
- Notifications via scheduler; status surfaces show last/next run without blocking UI.
- Audit status/reassignment/escalation; masking in exports/logs.

### Story 11.2 Notification Scheduler Reliability
User Story: As an ops owner, I want reliable notification scheduling so that alerts are delivered within SLOs.
Acceptance:
- Retries/backoff with bounded attempts and idempotency; duplicate/overlapping runs prevented.
- Status surface shows backlog/failures with remediation guidance; alerts on failure within threshold.
- Logs/telemetry with correlation IDs; rotation/retention defined; test harness supported.
