# Expanded Epic User Stories

## EPIC 1 - Authentication, Licensing & Startup Pipeline
### Story 1.1 Licensing/SSO Gate and Startup
User Story: As an operations admin, I want startup licensing and SSO gating so that only authorized users can open modules.
Acceptance:
- Block startup and module entry when PassNet/SSO/license validation fails; show remediation guidance and audit outcome.
- Enforce per-module license flags and hide/deny unauthorized modules; log attempts with correlation IDs.
- Telemetry captures auth/config/network errors; flows are non-blocking and retry-safe.

### Story 1.2 MSI/Version Preflight and Rollback
User Story: As a desktop engineer, I want MSI/version and dependency preflight so that upgrades do not break the shell.
Acceptance:
- Detect arch mismatch and missing MSI/DLLs (ComponentOne/Spread/TX/controls) and block with actionable guidance.
- Provide rollback path and record version/build info in audit/telemetry.
- Preflight runs without freezing UI and produces structured status (pass/warn/fail).

## EPIC 2 - Shell / MDI Application Framework
### Story 2.1 MDI Shell and Navigation
User Story: As a user, I want a themed MDI shell with navigation so that I can open modules and status surfaces predictably.
Acceptance:
- Navigation (tree/outbar/toolbars) and status bar respect permissions; unauthorized modules hidden/blocked.
- Windows open/restore/close reliably with remembered layout; no leaks or orphaned child windows.
- Theming aligns with ComponentOne styles; shell remains responsive while loading modules.

### Story 2.2 Background Worker UX
User Story: As a user, I want long-running UI actions to run in the background so that the shell stays responsive.
Acceptance:
- Long jobs use background worker patterns with progress/status surfaces; no UI thread blocking.
- Duplicate/overlapping runs prevented; safe cancellation where applicable with user guidance.
- Telemetry/logging captures lifecycle with correlation IDs and error taxonomy.

## EPIC 3 - Customer Management
### Story 3.1 Customer Search and Create with Deduplication
User Story: As a CSR, I want fast customer search and create with duplicate detection so that records stay clean.
Acceptance:
- Search/open under target SLA; create/edit/audit all changes.
- Duplicate detection on create/update with guidance to merge or cancel.
- Permissions enforced; masking applied to sensitive fields in UI/exports.

### Story 3.2 Customer Segmentation and Related Entities
User Story: As a relationship manager, I want to assign segments and view related entities so that I see customer context quickly.
Acceptance:
- Segments/tiers can be assigned/edited with audit; role-based visibility enforced.
- Related loans/collateral/docs surfaced with quick navigation.
- Exports respect masking rules and permissions.

## EPIC 4 - Loan Management
### Story 4.1 Loan Lifecycle (Create, Approval, Boarding)
User Story: As a loan officer, I want structured loan lifecycle steps so that approvals and boarding are controlled and auditable.
Acceptance:
- Create/edit/lock loans with required validations; status transitions recorded with audit.
- Lock/version behavior prevents concurrent edit conflicts and guides resolution.
- Boarding/approval blocks on missing critical data; UI guidance provided.

### Story 4.2 Risk, Covenants, and Narratives
User Story: As a risk analyst, I want to manage ratings, covenants, and narratives so that risk posture is tracked.
Acceptance:
- Capture ratings/covenants/narratives with audit; permissions enforced.
- Alert on breached covenants; views highlight exceptions.
- Reports/exports include data with masking for sensitive fields.

## EPIC 5 - Collateral Management
### Story 5.1 Collateral Registry and Relationships
User Story: As a collateral specialist, I want a registry linking collateral to multiple loans so that coverage is clear.
Acceptance:
- Register collateral with uniqueness/ID validation; link to multiple loans with coverage metrics.
- Permissioned views prevent unauthorized edits/deletes; cannot delete when in use.
- Audit all create/edit/link actions.

### Story 5.2 Appraisals and Coverage Rules
User Story: As a collateral reviewer, I want to record appraisals and enforce coverage rules so that LTV is maintained.
Acceptance:
- Record valuations with dates/source/history; maintain previous values.
- Enforce coverage/LTV rules and alert on breaches; guided remediation.
- Exports/appraisal reports audited; masking applied where required.

## EPIC 6 - Deposit Management
### Story 6.1 Accounts and Transactions
User Story: As a deposit analyst, I want to view account lifecycle and transactions so that I can service customers efficiently.
Acceptance:
- Show balances/history with filter/sort; performance meets UI SLA.
- Audit changes; masking for sensitive data.
- Permissions govern visibility and export.

### Story 6.2 Imports and Reconciliation
User Story: As an ops user, I want deposit imports and reconciliation to be reliable so that errors are caught early.
Acceptance:
- Imports validate schema, detect duplicates, and support idempotent runs.
- Reversals/adjustments handled with guided errors; background processing avoids UI blocking.
- Telemetry/audit for each run with error taxonomy.

## EPIC 7 - Documentation Tracking (DT)
### Story 7.1 Doc Templates and Assignment
User Story: As a doc coordinator, I want templates and assignments tracked so that requirements are clear per entity.
Acceptance:
- Manage templates; assign/reassign to loans/customers/collateral with audit.
- Track status/aging buckets accurately; waivers require reason/author/timestamp.
- Visibility controlled by permissions; exports respect masking.

### Story 7.2 Enforcement, Approvals, and Bulk Actions
User Story: As an approver, I want enforcement and bulk actions so that docs are complete before approval.
Acceptance:
- Enforce doc requirements before approval/boarding; configurable block/warn.
- Dashboards show exceptions/aging with exports; bulk assign/waive actions audited and limited.
- Temp/output hygiene for evidence paths; access to attachments logged.

## EPIC 8 - Notes & Memos
### Story 8.1 Rich Notes with Audit and Visibility
User Story: As a user, I want rich notes with audit and visibility controls so that collaboration is compliant.
Acceptance:
- Constrained rich text with author/timestamp; audit create/edit/soft-delete/version behavior.
- Visibility scope enforced; unauthorized deletes blocked; masking in exports/search.
- Performance aligns to search/open SLA; no UI freezes.

## EPIC 9 - Letters & Template Management
### Story 9.1 Template Library and Batch Generation
User Story: As a communications user, I want letter templates and batch generation so that outputs are consistent and auditable.
Acceptance:
- Manage template library/versioning with merge fields; preview before publish.
- Batch/group generation supports print/PDF/export with permissions/masking.
- Audit publishes/rollbacks and dependency checks for required DLLs/resources.

## EPIC 10 - Reports & Dashboards
### Story 10.1 Reporting and Queueing
User Story: As a reporting user, I want parameterized reports with queueing so that long jobs do not block UI.
Acceptance:
- C1 FlexReports accept parameters and queue long jobs with status/progress.
- Exports (PDF/Excel/CSV) respect masking/permissions; prevent duplicate/overlapping runs.
- Telemetry/error taxonomy logged; UI remains responsive.

### Story 10.2 Dashboards
User Story: As a manager, I want dashboards of key KPIs so that I can monitor operations quickly.
Acceptance:
- KPIs include exceptions/aging, scheduler health, licensing, report/import/OCR queues.
- Refresh configurable; views role-scoped; exports audited and masked.
- Performance avoids UI blocking; alert thresholds definable.

## EPIC 11 - Follow-up Tasks & Notification
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

## EPIC 12 - Financial Analysis (FA / Spread Module)
### Story 12.1 Spread Templates and Ratios
User Story: As a financial analyst, I want spread templates and ratios managed so that analyses are consistent.
Acceptance:
- Manage templates; compute ratios with validated inputs; save/load analyses with audit.
- Export summaries with masking; permissioned access enforced.
- Error handling and logging for calculations; performance meets SLA.

## EPIC 13 - Board Reports (BR)
### Story 13.1 Board Report Generation
User Story: As a reporting analyst, I want to generate board reports so that compliance and oversight needs are met.
Acceptance:
- Generate Past Due/Non-Accrual/One-Obligor and related BR reports with parameter validation.
- Use BR DB connectivity securely; role-based access enforced; audit pulls/exports.
- Retention policies applied to outputs/logs; masking where required.

## EPIC 14 - Board Report Scheduler / Windows Service
### Story 14.1 Scheduler Reliability
User Story: As an ops owner, I want BR scheduler reliability so that automated runs succeed without manual babysitting.
Acceptance:
- Automated schedules with retries/backoff; duplicate/overlapping runs prevented.
- Status surface shows last/next run, backlog, failures with remediation guidance; alerts on failures within SLO.
- Telemetry/logging with correlation IDs; supports dry-run/harness tests.

## EPIC 15 - OCR Pipeline (ABBYY)
### Story 15.1 ABBYY Batch OCR
User Story: As an imaging operator, I want ABBYY batch OCR with monitoring so that documents process reliably.
Acceptance:
- Folder monitoring with input validation; batch processing off UI thread.
- Error/retry handling with taxonomy; audit/log outcomes; retries bounded.
- Temp hygiene (secure/writable; cleanup after processing); masking for sensitive data.

## EPIC 16 - AI Tax Document Extraction (Azure Document Intelligence)
### Story 16.1 AI Extraction with Fallback
User Story: As an analyst, I want AI tax extraction with fallback so that field mapping is accurate and resilient.
Acceptance:
- Extract fields and map to codes; support multipage/multi-occur; validate schema.
- Fallback to ABBYY on failure; retries/backoff for transient errors; track accuracy.
- Secure key handling; audit/telemetry with correlation IDs; no secrets in logs.

## EPIC 17 - ComplianceOne Integration
### Story 17.1 File Exchange and Recovery
User Story: As an integrations engineer, I want robust ComplianceOne file exchange so that transfers are reliable and recoverable.
Acceptance:
- Validate IN/OUT paths and mappings; enforce version compatibility.
- Error recovery/manual retry for partial transfers; checksum/size validation when available.
- Logging/audit with error taxonomy; masking for sensitive data; retention/cleanup rules for exchanged files.

## EPIC 18 - Credit Bureau Integration
### Story 18.1 Bureau Request/Response Handling
User Story: As a credit officer, I want bureau integrations that are reliable and compliant so that pulls and responses are correct.
Acceptance:
- Validate requests; handle timeouts/retries/backoff; prevent duplicate pulls.
- Parse/mask responses; enforce compliance rules; audit pulls/exports.
- Status tracking and alerting on failures/downtime; retention/cleanup for responses/logs with PII.

## EPIC 19 - Square1 Portal Integration
### Story 19.1 Portal Connectivity and Access
User Story: As a portal admin, I want stable Square1 connectivity so that users can access portal resources securely.
Acceptance:
- Manage connectivity and session handling; enforce role-based access.
- Validate message flows; log/audit access and errors with taxonomy.
- Handle downtime/retries without UI blocking; alert on sustained failures.

## EPIC 20 - Mobile App TCP Integration
### Story 20.1 TCP Listener and Protocol
User Story: As a mobile services owner, I want a secure TCP listener so that mobile traffic on ports 5000-5100 is controlled.
Acceptance:
- Listener enforces auth/rate-limiting; validates protocol/version and message format; rejects malformed traffic.
- Handles heartbeats/timeouts/backpressure; logs with correlation IDs; alerts on repeated failures.
- Security constraints applied; test vectors documented for validation.

## EPIC 21 - Global Configuration Management
### Story 21.1 Config Admin and Audit
User Story: As an admin, I want safe configuration management so that paths/ports/timeouts/flags are governed.
Acceptance:
- Admin-only access to INI/app.config settings with validation; prevent invalid save; audit changes.
- Export/import config with masking of secrets; retain change history; rollbacks possible.
- Health check of config validity after changes with remediation guidance.

## EPIC 22 - Lookup Tables Management
### Story 22.1 Lookup CRUD and Integrity
User Story: As a data steward, I want managed lookup tables so that codes remain consistent.
Acceptance:
- CRUD with ordering/uniqueness; prevent delete when in use; permissions enforced.
- Bulk import/export with validation; audit all changes.
- Performance aligned to UI responsiveness; masking where needed in exports.

## EPIC 23 - SMTP & Email System Configuration
### Story 23.1 SMTP Setup and Test Mode
User Story: As an admin, I want SMTP configured with safe test modes so that email flows are reliable and controlled.
Acceptance:
- Configure host/port/SSL/TLS/credentials with protection and masking.
- Support test mode and debug logging/transcripts; rate limits/quiet hours configurable.
- Audit/test sends; error taxonomy for failures; no plaintext secrets in logs.

## EPIC 24 - User, Roles, Permission Management
### Story 24.1 Role-Based Access Control
User Story: As a security admin, I want role-based access control so that module and action access is governed.
Acceptance:
- Manage users (active/disabled) and roles; map permissions to modules/actions.
- Enforce least privilege; hide/deny unauthorized modules; audit role/permission changes.
- Exports and sensitive actions logged with correlation IDs; masking applied.

## EPIC 25 - Data Access Layer & SQL Connectivity
### Story 25.1 SqlClient-First Data Layer
User Story: As a platform engineer, I want standardized SQL connectivity so that data access is reliable and secure.
Acceptance:
- Standardize on SqlClient with timeouts and encrypted connections; handle legacy OLE DB safely.
- Centralize connection management; retry/backoff patterns defined; telemetry on DB failures.
- No breaking changes to existing APIs; masking for sensitive data in logs.

## EPIC 26 - Logging & Error Handling
### Story 26.1 Centralized Error Handling
User Story: As an engineer, I want centralized error handling so that failures are captured consistently.
Acceptance:
- Central error handler with Event Log integration and optional SMTP alerts; structured logging schema with correlation IDs.
- Error taxonomy applied across app/services; retention/rotation defined; debug logging safe for secrets.
- Validation that logs avoid PII unless masked; audit access to sensitive logs.

## EPIC 27 - Observability / Monitoring
### Story 27.1 Health and Monitoring
User Story: As an SRE, I want health and monitoring views so that service issues are detected quickly.
Acceptance:
- Surface health for schedulers/services; track job failures/retries; DB connectivity metrics shown.
- Alerting thresholds and routing defined; dashboards consume signals; heartbeats/synthetic checks configured.
- Observability configuration versioned; test harness to validate alert triggers.

## EPIC 28 - File System & Temporary Data Housekeeping
### Story 28.1 Temp/Data Hygiene
User Story: As an ops engineer, I want temp/data housekeeping so that storage and security stay under control.
Acceptance:
- Purge policies for OCR/AI temp folders; output retention rules enforced.
- Security ACLs on temp/output directories; audit cleanup actions; prevent deletions of in-use files.
- Telemetry/logs on cleanup outcomes and failures; non-blocking to UI.

## EPIC 29 - Security & Privacy Controls
### Story 29.1 PII and Secret Handling
User Story: As a security owner, I want PII masking and secret management so that privacy/compliance standards are met.
Acceptance:
- Mask SSN/TIN and sensitive fields in UI/logs/exports; enforce access control boundaries.
- Secrets managed outside source control; encrypted at rest/in transit; rotation procedures documented.
- Audit sensitive access and changes; retention/masking rules documented per data type.

## EPIC 30 - Upgrade & Deployment Management
### Story 30.1 MSI Deployment and Rollback
User Story: As a release manager, I want controlled MSI deployment so that upgrades are safe and reversible.
Acceptance:
- MSI installer paths support x64/x86 with network backend; version check/prompt flow with rollback steps.
- Environment chain (ST.Main.INI -> Suntell.ini) validated; preflight upgrade checks logged.
- Audit upgrade/rollback actions; failure guidance provided.

## EPIC 31 - Disaster Recovery & Backup Requirements
### Story 31.1 DR/Backup Execution
User Story: As a continuity planner, I want DR/backup procedures defined and tested so that recovery goals are met.
Acceptance:
- Define RPO/RTO targets for LMS/BR DB; test restore procedures regularly.
- Backup config (INI/app.config, MSI artifacts, license assets) documented; restore steps and verification recorded.
- Service restart runbooks; post-restart health/heartbeats verified.

## EPIC 32 - Performance & Capacity Management
### Story 32.1 Performance Targets
User Story: As a performance owner, I want defined targets and monitoring so that the app stays responsive under load.
Acceptance:
- Define targets for startup, search, report runtime, AI/OCR throughput, scheduler concurrency.
- Instrument and monitor against targets; alert on sustained breaches; capacity planning assumptions captured.
- Load test plans for key flows with thresholds; hardware/environment assumptions documented.

## EPIC 33 - Testing, QA & Acceptance Criteria
### Story 33.1 QA Coverage and Gates
User Story: As a QA lead, I want clear test coverage and gates so that releases meet agreed quality.
Acceptance:
- Define functional/negative, integration, performance/regression, and smoke expectations per environment.
- Tie stories to acceptance criteria and local testability guidance; track results/defects; gate readiness based on criteria.
- Include harness usage where applicable; ensure test data masking; exit criteria per release documented.

## EPIC 34 - Technical Debt & Migration Backlog
### Story 34.1 Migration Plan
User Story: As an architect, I want a migration backlog so that debt (OLE DB, secrets in configs, monolithic frmMDI) is reduced safely.
Acceptance:
- Prioritize items with impact/risk notes and completion acceptance; include move to SqlClient and PackageReference modernization.
- Plan for structured logging enhancements and refactor hotspots; dependencies identified.
- Migration steps avoid breaking changes; rollback/mitigation documented.

## EPIC 35 - Third-Party Component Management
### Story 35.1 Component Validation
User Story: As a platform owner, I want component validation so that third-party dependencies stay licensed and present.
Acceptance:
- Validate ComponentOne, TX Text Control, ABBYY, Azure DI, GrapeCity Spread licensing and DLL presence per arch.
- Preflight and runtime checks with audits/logs; block on critical missing/invalid licenses.
- Track component versions and renewal/expiry dates with alerting.

## EPIC 36 - Suntell GPT Assistant
### Story 36.1 Chat Shell and Azure OpenAI Integration
User Story: As a support rep, I want an embedded chat shell that talks to Azure OpenAI so that I can get quick help without leaving the MDI app.
Acceptance:
- ChatWidgetForm hosted inside frmMDI with header drag, FlowLayoutPanel transcript, and input bar with Enter-to-send; resizes with MDI layout and does not interfere with existing window lifecycle.
- Config-driven Azure settings (endpoint, deployment/model, API key) loaded from config/INI; no hardcoded secrets; validation errors surfaced with user-friendly guidance.
- Request pipeline uses async calls with last 6-message context and targets <=2s average response; displays bot/human messages, inline errors, and prevents duplicate sends while in flight.
- Graceful handling for network/429/timeout/unavailable responses; shows AI unavailable banner and disables automation affordances when backend is down.
- Telemetry captures intent request metadata (no PII), latency, and failures using existing logging pattern.

### Story 36.2 Intent Handling with Safe FlaUI Automation
User Story: As a support rep, I want the assistant to propose safe automations so that I can navigate and update the app faster without unintended changes.
Acceptance:
- Parse structured JSON responses to extract intent name, parameters, and automation steps; ignore or strip unknown or malformed fields safely.
- Surface automation CTA only when intent is actionable; state-changing actions require explicit confirmation; read-only intents may run directly per safety rules.
- Validate selected customer/context and target form AutomationId/Name before executing; abort with guidance on mismatch or missing elements.
- Execute FlaUI automation asynchronously with success/failure status, logs, and remediation hints; failures avoid partial writes and leave the UI responsive.
- Automation events recorded via existing telemetry/logging (no PII), including intent, outcome, latency, and error details.

### Story 36.3 Context Persistence and Resiliency
User Story: As a support rep, I want chat context and customer alignment to persist so that I can resume conversations and automations reliably.
Acceptance:
- Persist chat history per user session (recent messages) to disk or configured storage; exclude secrets and enforce rotation/size limits.
- On restart, rehydrate conversation and restore assistant state; tie context to the currently selected customer and prompt to reselect if mismatched.
- Provide explicit AI unavailable/offline state when Azure/OpenAI cannot be reached; hide or disable automation CTAs while offline.
- Ensure history and telemetry handling respect PII rules; no customer-sensitive data stored in plain text logs.
- Persistence and offline flows are non-blocking and do not break existing MDI navigation or module loading.
