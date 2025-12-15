# Epic Stories

### EPIC 1 — Authentication, Licensing & Startup Pipeline
#### Story 1.1 Licensing/SSO Gate and Startup
- Enforce PassNet licensing/SSO on startup and module entry; block on failure with guidance and audit.
- Feature gating per license flags; unauthorized modules hidden/blocked with audit.
- Telemetry with correlation IDs and error taxonomy (auth/config/network).

#### Story 1.2 MSI/Version Check and Rollback
- Detect arch (x64/x86) and use correct MSI paths; block on mismatch/missing package with remediation.
- Validate DLLs (ComponentOne/Spread/TX/Controls/Graphics) post-update; log missing/invalid licenses.
- Provide rollback steps and audit/version check events.

#### Story 1.3 Preflight Config/Dependency Diagnostics
- Validate INI/app.config keys, DLLs, ports (5000–5100), licensing assets, temp/output directories.
- Emit structured preflight report (pass/fail with guidance); block on critical failures.
- Secure temp hygiene and key handling; logs with correlation IDs.

#### Story 1.4 Startup Telemetry and Health
- Emit telemetry for licensing checks and scheduler heartbeats; health surfaces show state/last/next run.
- Alert thresholds detect failures <5 minutes; log rotation/retention defined.
- Recovery runbook links for licensing/scheduler failures.

### EPIC 2 — Shell / MDI Application Framework
#### Story 2.1 MDI Shell and Navigation
- Provide MDI shell with navigation (tree/outbar/toolbars) and status bar; theme aligned to ComponentOne.
- Support window lifecycle (open/close/restore) with permissions-driven visibility.
- Non-blocking background worker hooks for long tasks.

#### Story 2.2 Background Worker UX
- Run long jobs (reports/imports/OCR) off the UI thread with progress/status surfaces.
- Allow cancellation where safe; prevent duplicate/overlapping runs.
- Telemetry/logging for job lifecycle with correlation IDs.

### EPIC 3 — Customer Management
#### Story 3.1 Customer Search and Create with Deduplication
- Search/create/edit customers with <2s search/open target; audit all changes.
- Duplicate detection on create/update with guidance to merge/cancel.
- Capture KYC/ID fields and required validations.

#### Story 3.2 Customer Segmentation and Related Entities
- Assign segments/tiers; surface related loans/collateral/docs overview.
- Permissions-controlled visibility; exports respect masking rules.
- Telemetry on segment changes and related-entity navigation.

### EPIC 4 — Loan Management
#### Story 4.1 Loan Lifecycle (Create → Approval → Boarding)
- Create/edit/lock loans; track status transitions through approval/boarding with audit.
- Enforce required fields and validations; block on missing critical data.
- Version/lock behavior prevents concurrent edits; surface conflict guidance.

#### Story 4.2 Risk, Covenants, and Narratives
- Capture risk ratings, covenants, narratives; audit changes.
- Alert on breached covenants; permissioned visibility.
- Include in reports/exports with masking for sensitive data.

#### Story 4.3 Renewals and Modifications
- Support renewals/mods with linkage to prior loans; carry forward key fields.
- Audit deltas and approval steps; prevent duplication of active records.
- Telemetry on renewals volume and outcomes.

#### Story 4.4 Financial Calculations
- Compute LTV/DSCR/schedules with validation of inputs; show assumptions.
- Recalculate on input change; log calculation errors.
- Allow export of calculation summaries with masking where needed.

### EPIC 5 — Collateral Management
#### Story 5.1 Collateral Registry and Relationships
- Register collateral, link to multiple loans; enforce uniqueness/ID validation.
- Surface coverage metrics per linked loans; audit create/edit.
- Permissioned views; prevent delete when in use.

#### Story 5.2 Appraisals and Coverage Rules
- Record appraisals/valuations with dates/sources; maintain history.
- Enforce coverage/LTV rules; alert on breach.
- Export/appraisal reports with masking/audit of access.

### EPIC 6 — Deposit Management
#### Story 6.1 Accounts and Transactions
- View account lifecycle, balances, transaction history; filter/sort quickly.
- Audit all changes; masking for sensitive fields.
- Performance targets align with search/open SLA.

#### Story 6.2 Imports and Reconciliation
- Import/reconcile deposits with schema validation, duplicate detection, idempotency.
- Handle reversals/adjustments and mismatches with guided errors.
- Background processing; telemetry and audit of runs.

### EPIC 7 — Documentation Tracking (DT)
#### Story 7.1 Doc Templates and Assignment
- Manage doc requirement templates; assign/reassign to loans/customers/collateral.
- Track status/aging buckets; accurate aging calculations.
- Audit all changes; waivers require reason/author/timestamp.

#### Story 7.2 Enforcement and Approvals
- Enforce doc requirements before loan approval/boarding; block or warn per policy.
- Exceptions/aging dashboards with exports (permissioned/masked).
- Notifications/hooks for overdue/waiver events.

#### Story 7.3 Evidence and Bulk Actions
- Attach evidence/file paths; validate accessible locations.
- Bulk actions (assign, waive) with audit and limits.
- Temp/output hygiene for uploads; log access to attachments.

### EPIC 8 — Notes & Memos
#### Story 8.1 Rich Notes with Audit and Visibility
- Constrained rich text; author/timestamp; visibility controls.
- Audit create/edit/soft-delete/version behavior; prohibit unauthorized deletes.
- Exports/search respect masking; performance aligns to search/open SLA.

### EPIC 9 — Letters & Template Management
#### Story 9.1 Template Library and Batch Generation
- Manage template library/versioning with merge fields; preview before publish.
- Batch/group letter generation with print/PDF/export; enforce masking/permissions.
- Audit publishes/rollbacks; dependency checks for required DLLs/resources.

### EPIC 10 — Reports & Dashboards
#### Story 10.1 Reporting and Queueing
- C1 FlexReports with parameters; queue long jobs; non-blocking UI with status.
- Exports PDF/Excel/CSV with permissions/masking; audit sensitive exports.
- Telemetry/error taxonomy; prevent duplicate/overlapping runs.

#### Story 10.2 Dashboards
- Dashboard KPIs: exceptions/aging, scheduler health, licensing, report runs, imports/OCR queues, follow-ups.
- Configurable refresh; role-scoped views; audit/permissions on exports.
- Performance targets to avoid UI blocking.

### EPIC 11 — Follow-up Tasks & Notification 
#### Story 11.1 Tasks, Reminders, and Notifications 
- Create/assign tasks with due dates/status; escalations/reminders configurable. 
- Notifications via scheduler; status surfaces without blocking UI. 
- Audit status/reassignment/escalation; masking in exports/logs. 

#### Story 11.2 Notification Scheduler Reliability 
- Implement retries/backoff with bounded attempts and idempotency for notifications; classify errors (IO/API/Parsing/Quota/Config). 
- Status surface: last/next run, backlog, recent failures with remediation guidance; no UI blocking. 
- Logs/telemetry with correlation IDs; alert on failure per SLO (detect <5 minutes); rotation/retention set. 
- Recovery actions/runbook steps documented; support NotificationTester for test mode. 
- Prevent duplicate/overlapping runs; background worker behavior validated. 

### EPIC 12 — Financial Analysis (FA / Spread Module) 
#### Story 12.1 Spread Templates and Ratios 
- Manage spread templates; compute ratios; save/load analyses. 
- Validate inputs/mapping; audit changes. 
- Export summaries with masking and audit of access. 

### EPIC 13 — Board Reports (BR)
#### Story 13.1 Board Report Generation
- Generate Past Due/Non-Accrual/One-Obligor and related BR reports.
- Use BR DB connectivity; parameter validation and role-based access.
- Audit/report outputs with retention policies.

### EPIC 14 — Board Report Scheduler / Windows Service 
#### Story 14.1 Scheduler Reliability 
- Automated schedules with retries/backoff; prevent duplicate/overlapping runs. 
- Status surface (last/next run, backlog, failures) with remediation guidance. 
- Telemetry/logging with correlation IDs; alert on failures within SLO; support BRTestGen/dry-run harness. 

### EPIC 15 — OCR Pipeline (ABBYY)
#### Story 15.1 ABBYY Batch OCR
- Batch OCR processing with folder monitoring; validate inputs/paths.
- Error/retry handling with taxonomy; audit/log outcomes.
- Temp hygiene (secure/writable; cleanup after processing).

### EPIC 16 — AI Tax Document Extraction (Azure Document Intelligence)
#### Story 16.1 AI Extraction with Fallback
- Extract tax fields with XML mapping to internal codes; multipage/multi-occur support.
- Fallback to ABBYY on failure; retries/backoff where safe; accuracy tracking.
- Secure key handling; audit/telemetry with correlation IDs.

### EPIC 17 — ComplianceOne Integration 
#### Story 17.1 File Exchange and Recovery 
- IN/OUT paths validated; field mapping applied; version compatibility checked. 
- Error recovery/manual retry for partial transfers; checksum/size validation when available. 
- Logging/audit with error taxonomy; masking for sensitive data; retention/cleanup rules for exchanged files. 

### EPIC 18 — Credit Bureau Integration 
#### Story 18.1 Bureau Request/Response Handling 
- Validate requests; handle timeouts/retries/backoff; prevent duplicate pulls. 
- Parse/mask responses; enforce compliance rules; audit pulls/exports. 
- Status tracking and alerting on failures/downtime; retention/cleanup for bureau responses and logs containing PII. 

### EPIC 19 — Square1 Portal Integration
#### Story 19.1 Portal Connectivity and Access
- Manage portal connectivity and session handling; enforce role-based access.
- Validate message/interaction flows; log/audit access and errors.
- Handle downtime/retries without UI blocking.

### EPIC 20 — Mobile App TCP Integration 
#### Story 20.1 TCP Listener and Protocol 
- Operate TCP listener on ports 5000–5100 with auth/rate limiting. 
- Validate message protocol/version and message formats; handle heartbeats/timeouts/backpressure; reject malformed traffic. 
- Enforce security constraints and connection monitoring; capture rate-limit events. 
- Log/telemetry with correlation IDs; alert on repeated failures; document test vectors for protocol validation. 

### EPIC 21 — Global Configuration Management 
#### Story 21.1 Config Admin and Audit 
- Manage INI/app.config settings (paths, ports, timeouts, flags) with admin-only access. 
- Validate paths/values; prevent invalid save; audit changes. 
- Export/import config with masking of secrets; retain change history. 
- Config changes logged with user/timestamp; rollbacks possible. 
- Health check of config validity after changes with clear remediation guidance. 

### EPIC 22 — Lookup Tables Management
#### Story 22.1 Lookup CRUD and Integrity
- CRUD for lookup codes with ordering/uniqueness; prevent delete when in use.
- Bulk import/export with validation; audit changes.
- Performance aligned to UI responsiveness.

### EPIC 23 — SMTP & Email System Configuration
#### Story 23.1 SMTP Setup and Test Mode
- Configure SMTP host/port/SSL/TLS/credentials with protection and masking.
- Support test mode and debug logging/transcripts; rate limits/quiet hours configurable.
- Audit/test sends; error taxonomy for failures.

### EPIC 24 — User, Roles, Permission Management
#### Story 24.1 Role-Based Access Control
- Manage users (active/disabled) and roles; map permissions to modules/actions.
- Enforce least privilege; hide/deny unauthorized modules; audit role/permission changes.
- Exports and sensitive actions logged with correlation IDs.

### EPIC 25 — Data Access Layer & SQL Connectivity
#### Story 25.1 SqlClient-First Data Layer
- Standardize on SqlClient with timeouts and encrypted connections; handle legacy OLE DB safely.
- Centralize connection management; retry/backoff patterns defined.
- Telemetry on DB failures; logging with error taxonomy.

### EPIC 26 — Logging & Error Handling 
#### Story 26.1 Centralized Error Handling 
- Central error handler with Event Log integration and optional SMTP alerts. 
- Structured logging schema with correlation IDs; retention/rotation defined. 
- Error taxonomy applied across app/services; include failure severities and destinations. 
- Ability to enable debug logging in test mode without exposing secrets. 
- Validation that logs avoid PII unless masked; audit access to sensitive logs. 

### EPIC 27 — Observability / Monitoring 
#### Story 27.1 Health and Monitoring 
- Service health status for schedulers/services; job failure/retry tracking. 
- AI/OCR failure tracking; DB connectivity metrics surfaced. 
- Alerting thresholds and routing defined; dashboards consume signals. 
- Heartbeat endpoints and synthetic checks for schedulers/licensing; notify on stale heartbeats. 
- Observability configuration versioned; test harness to validate alert triggers. 

### EPIC 28 — File System & Temporary Data Housekeeping
#### Story 28.1 Temp/Data Hygiene
- OCR/AI temp folder purge policies; output retention rules enforced.
- Security ACLs on temp/output directories; audit cleanup actions.
- Telemetry/logs on cleanup outcomes and failures.

### EPIC 29 — Security & Privacy Controls 
#### Story 29.1 PII and Secret Handling 
- Mask SSN/TIN and sensitive fields in UI/logs/exports; enforce access control boundaries. 
- Secrets managed outside source control; encrypted at rest/in transit per policy. 
- Audit sensitive access and changes; penetration/abuse case logging readiness. 
- Retention/masking rules documented per data type; exports gated by permissions. 
- Secret rotation procedures and key storage locations documented; validation checks in preflight. 

### EPIC 30 — Upgrade & Deployment Management
#### Story 30.1 MSI Deployment and Rollback
- MSI installer paths with arch-specific handling (x64/x86) and network backend support.
- Version check/prompt flow with rollback procedures; audit upgrade/rollback actions.
- Environment chain (ST.Main.INI → Suntell.ini) validated; preflight upgrade checks logged.

### EPIC 31 — Disaster Recovery & Backup Requirements
#### Story 31.1 DR/Backup Execution
- Define RPO/RTO targets for LMS/BR DB; test restore procedures.
- Backup config (INI/app.config, MSI artifacts, license assets); document restore steps.
- Service restart runbooks; verify post-restart health/heartbeats.

### EPIC 32 — Performance & Capacity Management 
#### Story 32.1 Performance Targets 
- Startup/splash-to-shell, search, report runtime, AI/OCR throughput, scheduler concurrency targets defined. 
- Instrument and monitor against targets; alert on sustained breaches. 
- Capacity planning assumptions documented; periodic review cadence set. 
- Load test plans for key flows (search, reports, OCR/imports, schedulers) with target thresholds. 
- Capture hardware/environment assumptions and scaling guidance. 

### EPIC 33 — Testing, QA & Acceptance Criteria 
#### Story 33.1 QA Coverage and Gates 
- Define functional/negative, integration, performance/regression, and smoke test expectations per environment. 
- Tie stories to acceptance criteria and local testability guidance. 
- Track test results and defects; gate readiness based on agreed criteria. 
- Include test harness usage (NotificationTester, BRTestGen) where applicable; ensure test data masking. 
- Define exit criteria per release including regression scope and environment sign-offs. 

### EPIC 34 — Technical Debt & Migration Backlog
#### Story 34.1 Migration Plan
- Backlog to migrate off OLE DB to SqlClient; remove secrets from configs; refactor frmMDI hotspots.
- Plan PackageReference modernization and structured logging enhancements.
- Prioritize debt items with impact/risk notes and acceptance for completion.

### EPIC 35 — Third-Party Component Management
#### Story 35.1 Component Validation
- Validate ComponentOne, TX Text Control, ABBYY, Azure DI, GrapeCity Spread licensing and DLL presence per arch. 
- Preflight and runtime checks with audits/logs; block on critical missing/invalid licenses. 
- Track component versions and renewal/expiry dates with alerting. 


### EPIC 36 - Suntell GPT Assistant
#### Story 36.1 Chat Shell and Azure OpenAI Integration
- ChatWidgetForm UI hosted in frmMDI; secure config for Azure endpoint/deployment/key.
- Request/response flow with errors surfaced to users; Enter-to-send and responsive layout maintained.

#### Story 36.2 Intent Handling with Safe FlaUI Automation
- Parse structured intent JSON; show actionable links that require confirmation for state changes.
- Execute FlaUI automations with AutomationId/Name validation and success/failure logging.

#### Story 36.3 Context Persistence and Resiliency
- Persist chat history per user session and rehydrate on restart.
- Tie context to selected customer; offline/AI-unavailable messaging disables automations safely.
