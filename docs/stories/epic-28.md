# EPIC 28 - File System & Temporary Data Housekeeping

### Story 28.1 Temp/Data Hygiene
User Story: As an ops engineer, I want temp/data housekeeping so that storage and security stay under control.
Acceptance:
- Purge policies for OCR/AI temp folders; output retention rules enforced.
- Security ACLs on temp/output directories; audit cleanup actions; prevent deletions of in-use files.
- Telemetry/logs on cleanup outcomes and failures; non-blocking to UI.
