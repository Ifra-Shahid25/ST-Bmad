# EPIC 14 - Board Report Scheduler / Windows Service

### Story 14.1 Scheduler Reliability
User Story: As an ops owner, I want BR scheduler reliability so that automated runs succeed without manual babysitting.
Acceptance:
- Automated schedules with retries/backoff; duplicate/overlapping runs prevented.
- Status surface shows last/next run, backlog, failures with remediation guidance; alerts on failures within SLO.
- Telemetry/logging with correlation IDs; supports dry-run/harness tests.
