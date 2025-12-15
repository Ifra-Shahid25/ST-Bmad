# ST Loan Management System (ST Main) Product Requirements Document (PRD) 
 
## Goals and Background Context 
 
### Goals 
- Enforce PassNet licensing and SSO up front so only authorized users/modules run. 
- Centralize customer, loan, collateral workflows with fast search/create and auditable changes. 
- Reduce documentation exceptions and overdue items through assignments, aging, and waiver tracking. 
- Improve reliability and observability of schedulers (notifications, board reports) with retries, alerts, and diagnostics. 
- Provide resilient reporting (C1 FlexReport/board reports) and notifications that avoid blocking the UI. 
- Deliver accurate OCR/AI extraction for tax forms with mapping, review flows, and cleanup for temp files. 
- Harden installs/updates with version checks, arch-specific MSI/DLL validation, and rollback guidance. 
- Enhance imports (LMSImport) with schema validation, duplicate detection, idempotency, and clear error reporting. 
- Support secure templates/letters publishing with role-based access, validation, and version control. 
- Increase operational visibility via preflight/config checks, telemetry, and audit trails across key entities. 
 
### Background Context 
The existing WinForms/.NET Framework 4.8 LMS serves lenders, credit teams, compliance, and operations. It spans customers, loans, collateral, documentation tracking, notes/memos, reports, schedulers, and integrations (Credit Bureau, ComplianceOne, Square1 Portal, mobile TCP). Current pain points include fragile schedulers and licensing checks, configuration drift (INI/app.config), missing DLLs, limited observability, and slow reporting or onboarding when configs mismatch. The MVP keeps the on-prem WinForms footprint, enforces licensing/feature gating at startup and module entry, and hardens reliability for schedulers, document tracking, and reporting while integrating OCR/AI extraction, imports, and template publishing. Telemetry, retries/backoff, and preflight diagnostics are needed to reduce MTTR and ensure compliance/auditability without a major rewrite. 
 
### Change Log 
| Date       | Version | Description                                  | Author | 
|------------|---------|----------------------------------------------|--------| 
| 2025-12-03 | 0.1     | Initial PRD draft from project brief context | PM (John) | 
 
### Out of Scope 
- Non-Windows clients or cloud-native rewrite; remain on WinForms/.NET Framework 4.8. 
- PackageReference migration or broad architectural refactor. 
- Major UX redesign beyond incremental guardrails and clarity improvements. 
 
### MVP Validation Approach 
- Validate success via: licensing/SSO gating rates; doc exception/aging reductions; scheduler success/detection/recovery SLOs; report runtime targets; OCR/AI accuracy with review queue throughput; import success/error rates. 
- Collect telemetry for schedulers/licensing/OCR/imports; review exception/aging dashboards; run dry-run imports; sample OCR mappings with manual review. 
- Gather user feedback from loan ops, compliance, and IT/ops after each deploy; adjust backlog based on SLO deltas and exception trends. 

### Success Metrics (from brief) 
- Documentation exceptions: target <10% exception rate; reduce >30-day aged items by 30%. 
- Performance: search/open <2s; customer/loan create <2 minutes; splash-to-shell <5s; report/board report runtime <2 minutes. 
- Scheduler reliability: >=99.5% weekly success; detection <5 minutes; recovery <30 minutes. 
- Licensing/SSO: enforce 100% gating; success >99%. 
- Notifications: delivery >99%; recovery within 10 minutes of failure. 
- OCR/AI: mapped field accuracy >95% with manual review queue; processing <60s per batch where applicable. 
## Requirements 
 
### Functional 
1. FR1: Enforce PassNet licensing and SSO gating at startup and module entry; block mismatched versions; audit outcomes. 
2. FR2: Run preflight/config diagnostics (INI paths, ports, DLLs, connection strings, keys) with clear remediation guidance before allowing runtime. 
3. FR3: Customer search/create/edit with validation, audit trail, and <2s search/open targets. 
4. FR4: Loan and collateral management with linkage, required validations, narratives, and full audit history. 
5. FR5: Documentation tracking with assignments, statuses, exceptions/waivers (with reasons), aging/overdue views, reassignment, and follow-ups. 
6. FR6: Notes/memos with author/timestamp, constrained rich text, visibility/permissions, soft-delete with audit. 
7. FR7: Follow-ups/Tasks with due dates, notifications, status changes, and auditability. 
8. FR8: Reporting (C1 FlexReport) and dashboards with filters, exports, and role-based permissions. 
9. FR9: Board Report Scheduler service (BR DB) with retries/backoff, logging, and recovery/runbook support. 
10. FR10: Notification scheduler service with retries/backoff, status logging, and recovery flow. 
11. FR11: Health checks/telemetry for schedulers and licensing with alerting to ops (e.g., Event Log/sinks) and status surfacing. 
12. FR12: OCR/AI extraction for tax forms via ABBYY + Azure Document Intelligence with mapping to internal codes, error taxonomy, fallback-to-ABBYY, temp file hygiene, and manual review queue. 
13. FR13: LMSImport (CSV/Excel) with schema validation, duplicate detection/idempotency, dry-run, and clear error reporting. 
14. FR14: CustomTemplates/Letters with file validation, versioning/publishing, role-based access, merge/print/export flows. 
15. FR15: Deposits module with account views, balances, transaction history, imports/reconciliation with validation. 
16. FR16: Integrations: Credit Bureau requests; ComplianceOne file exchange with retries/recovery; Square1 Portal and mobile TCP server with auth, rate limits, message validation/logging. 
17. FR17: Background workers/queues for long-running jobs (reports, notifications, AI/OCR) to avoid UI blocking; surface job status. 
18. FR18: Version check + MSI prompt flow with arch-specific x64/x86 paths, mismatch handling, and rollback guidance. 
19. FR19: Audit trails for loans, docs/waivers, notes/memos, follow-ups capturing user/timestamp/old-new values; prohibited deletes. 
 
### Non Functional 
1. NFR1: Platform constraint - WinForms on .NET Framework 4.8 with `packages.config`; no cloud rewrite.
2. NFR2: Performance - search/open <2s; customer/loan create <2 minutes; splash-to-shell <5s; standard reports/board reports runtime <2 minutes.
3. NFR3: Reliability/SLOs - schedulers >=99.5% weekly success; detection <5 minutes; recovery <30 minutes.
4. NFR4: Security/Compliance - enforce licensing/SSO; encrypt secrets; mask SSN/TIN in UI/logs/exports; secure temp directories.
5. NFR5: Observability/Logging - telemetry for schedulers/licensing/health checks; structured logs with correlation IDs; retention/rotation defined.
6. NFR6: Data Retention/Housekeeping - temp OCR/AI directories cleaned; report/notification outputs retained per policy; log rotation; archive rules documented.
7. NFR7: Dependency Validation - ABBYY, ComponentOne, TX Text Control, GrapeCity Spread, Controls/Graphics DLLs validated per architecture with runtime license checks.
8. NFR8: Deployment/Upgrade - MSI packaging with arch detection; UNC/local backend path support; installer/update verification checklist; offline/air-gapped support; rollback steps.
9. NFR9: Background Job Safety - retries with backoff and idempotency; no UI blocking; rate limits for external services; error taxonomy (IO/API/Parsing/Quota) handled consistently.
10. NFR10: Privacy/Exports - role-based access and masking for exports/reports; audit sensitive access.
 
## User Interface Design Goals 
 
### Overall UX Vision 
Familiar WinForms MDI with speed and clarity prioritized over visual redesign. Keep search/open fast, surface documentation status/aging and scheduler/licensing/health indicators without clutter, and enforce guarded rich text rules for notes/memos. Favor non-blocking operations with clear job status. 
 
### Key Interaction Paradigms 
Ribbon/menu plus MDI workspace; docked panes for lists/details; background job status toasts/log panels; wizard-style preflight/config checks; non-blocking progress for OCR/imports/report generation; inline validation with audit prompts. 
 
### Core Screens and Views 
- Login/licensing gate 
- Dashboard with alerts (exceptions, scheduler health) 
- Customer/loan/collateral detail with linked docs/tasks/notes 
- Documentation tracking board/aging view 
- Scheduler status/controls (notifications, board reports) 
- Reporting/board report queues and outputs 
- Imports console (LMSImport) with schema check/dry-run 
- OCR/AI review and exception queue with mappings 
- Templates/letters management with publishing controls 
- Config/preflight diagnostics 
- Admin/audit reports 
 
### User Journeys and Edge Cases 
- Startup/licensing/version: splash â†’ config/licensing/SSO â†’ version/MSI check; handle missing DLLs, arch mismatch, and config errors with guided remediation. 
- Documentation tracking: assign/update docs, aging/overdue review, waiver with reason; handle reassignment conflicts and prohibited deletes. 
- Scheduler recovery: notification/board report status surfaces, retries/backoff, failed runs with remediation; avoid duplicate/overlapping runs. 
- OCR/AI review: submit docs, map fields, route low-confidence/failed to review queue; handle large files, quota/API failures, and temp cleanup. 
- Imports: schema validate, dry-run, idempotent live run; handle duplicates, malformed rows, and partial failures with clear errors. 
- Notes/follow-ups: constrained rich text, permissions, audit; handle soft-delete and masking in exports. 
- Reporting: non-blocking runs, status/progress, permissioned exports; handle long-running jobs and failure guidance. 
 
### Accessibility: WCAG AA 
Keyboard navigation, high-contrast theme option, and font scaling where feasible in WinForms. 
 
### Branding 
Match existing ST Main look (ComponentOne controls), no major restyle; ensure icons/fonts/DLL resources are validated and present. 
 
### Target Device and Platforms: Desktop Only 
Windows desktop only; responsive web not required. 
 
## Technical Assumptions 
 
### Repository Structure: Monorepo 
Single repo containing the WinForms app, shared modules, and supporting services/utilities; keep the existing module layout (Util, Data, Error, Customers, Loans, Collateral, DT, Reports, Dashboards, FollowUp, Configure, Lookup, FA, BR/BRSchedule, Credit Bureau, OCR/AI, Portal, TCP). 
 
### Service Architecture 
Monolith WinForms client with supporting Windows services (Notification, Board Report Scheduler); background workers/queues for long-running jobs; remain on .NET Framework 4.8 with `packages.config`. 
 
### Testing Requirements 
Unit and integration coverage for critical modules; harnesses for schedulers/imports (e.g., NotificationTester, BRTestGen) and import validation; manual regression for UI-heavy flows; telemetry-driven checks for schedulers/licensing. 
 
### Additional Technical Assumptions and Requests 
- ABBYY + Azure Document Intelligence keys/paths available; temp directories secured and cleaned. 
- ComponentOne/Spread/TX Text Control/Controls/Graphics DLLs validated per architecture (x86/x64) with runtime license checks. 
- INI chain `ST.Main.INI` -> `Suntell.ini` with `[LMS] BACKEND` for MSI/INI/docs; MSI shares may be local or UNC; arch-specific MSI folders (`MSI\\x64`, `MSI\\x86`). 
- Dual DB connections (LMS DB, BR DB) with encryption preferred; service accounts have Event Log/share/SMTP rights. 
- TCP ports 5000-5100 reserved for mobile/portal; enforce auth, rate limits, and logging. 
- Secrets not stored in plaintext; offline/air-gapped environments supported via bundled licensing assets/MSI shares. 
- Background jobs non-blocking; retries/backoff with idempotency and consistent error taxonomy (IO/API/Parsing/Quota). 
- Logging/telemetry sinks available with rotation/retention; correlation IDs for cross-service tracing. 

### Email Delivery Constraints 
- SMTP/STARTTLS auth required; rate limits and quiet hours configurable; retries/backoff with bounded attempts. 
- Error taxonomy applied (IO/API/Config); surface failures in scheduler status with remediation steps. 
- Audit/log notification sends with correlation IDs; mask sensitive content; support test mode (NotificationTester). 
 
### Architecture Guidance Updates 
- Telemetry/logging sinks: Event Log plus optional file/forwarder; structured logs with correlation IDs `{env}:{service}:{jobId}`. 
- Error taxonomy: IO/API/Parsing/Quota/Config/SQL applied across schedulers/OCR/imports. 
- MSI rollback: on failed update, revert to prior MSI from `[LMS] BACKEND`, re-validate DLLs per arch, and log/audit rollback with user/timestamp. 
- Dependency validation process: preflight DLL/license checks per arch (ComponentOne/Spread/TX/Controls/Graphics/ABBYY/Azure DI); block critical misses with guidance. 
- Temp hygiene: enforce secured, writable temp directories; clean after OCR/AI and imports; log cleanup outcomes. 
 
## Data Requirements and Retention 
- Entities: customers, loans, collateral, documentation items/waivers, notes/memos, follow-ups/tasks, reports/board reports, imports, OCR/AI extraction results, audit logs. 
- Retention: temp OCR/AI directories cleaned after processing; log rotation/retention per policy; report/notification outputs retained per agreed durations; masking for SSN/TIN in exports/logs. 
- Migration/backfill: none specified yet; confirm if existing data needs backfill for new fields (e.g., waivers, audit detail) before implementation. 

## Data Model Overview 
- Core entities: customers, loans, collateral, documentation items, waivers, notes/memos, follow-ups/tasks, users/roles, reports/board reports, imports, OCR/AI runs, audit logs. 
- Relationships: customers ↔ loans (1:N), loans ↔ collateral (1:N), loans/customers ↔ documentation items (1:N), documentation ↔ waivers (0:1), customers/loans ↔ notes/follow-ups (1:N), scheduler jobs ↔ report outputs (1:N), imports ↔ imported records (1:N with idempotency keys). 
- Sensitive fields: SSN/TIN, PII in notes/exports; must be masked in UI/logs/exports. 
- Identifiers: stable IDs for customers/loans/docs; idempotency keys for imports; correlation IDs for background jobs. 
- Audit scope: create/edit/status/waiver changes across docs/loans/collateral/notes/follow-ups; access to sensitive exports logged. 

## Roles and Permissions 
- Roles: Loan Officer, Documentation Specialist, Compliance/Risk, Reporting/Board User, IT/Ops, Admin. 
- Modules/actions: view/create/edit/delete per entity; waivers (create/view) restricted to Documentation/Compliance/Admin; scheduler controls (start/stop/retry/view backlog) for IT/Ops/Admin; imports (dry-run/live) for IT/Ops/Admin; OCR approvals for Documentation/Compliance; exports for Reporting/Compliance/Admin with masking; config/preflight for IT/Ops/Admin. 
- Principle: least privilege; permission checks enforced in UI and services; unauthorized modules hidden or blocked with audit entry. 

### Role Profiles 
- Loan Officer: owns customer/loan creation and updates; can add notes/follow-ups; cannot waive docs; limited exports. 
- Documentation Specialist: manages documentation assignments/aging/waivers; uploads evidence; initiates notifications; cannot change config. 
- Compliance/Risk: approves waivers, reviews audit trails, accesses masked exports, oversees bureau/ComplianceOne pulls. 
- Reporting/Board User: runs reports/board reports, views dashboards, limited to export permissions set by Compliance/Admin. 
- IT/Ops: manages configs, schedulers, imports, service health, and preflight/diagnostics; can run test modes (NotificationTester/BRTestGen). 
- Admin: full permissions including roles/permissions management, config changes, and emergency overrides with audit. 

## Dashboards Requirements 
- Widgets/KPIs: documentation exceptions/aging by bucket; scheduler health (notification/board reports) last/next run and failure counts; licensing status; report run status; imports queue (success/fail/dry-run); OCR review queue (pending/failed/age); follow-ups overdue/upcoming. 
- Refresh: manual refresh plus periodic refresh (configurable); do not block UI. 
- Permissions: dashboards scoped to role; sensitive counts (SSN/TIN data) masked; exports audited. 

## Disaster Recovery and Backup Plan 
- DB backups for LMS DB and BR DB with defined RPO/RTO targets (confirm with ops); test restore procedures; encrypt backups where applicable. 
- Back up configuration: INI/app.config, `[LMS] BACKEND` MSI artifacts (x64/x86), and third-party license assets; document restore steps. 
- Rollback: retain prior MSI packages; rollback procedure tested; audit rollback actions. 
- Logs and telemetry: rotation/retention defined; ensure availability for incident review; mask sensitive data. 
- Services: restart runbooks for Notification and Board Report schedulers; verify post-restart health/heartbeats. 

## Stakeholders and Communications 
- Stakeholders: Loan Ops/Credit, Documentation Specialists, Compliance/Risk, Reporting/Board users, IT/Ops (services/config/MSI), Engineering/QA. 
- Communications: PRD updates and approval via PM + key stakeholders; release/update notes to IT/Ops and user leads; incident/reliability updates routed to IT/Ops with scheduler/licensing telemetry summaries. 
 
## Epic List 

- EPIC 1 — Authentication, Licensing & Startup Pipeline: SSO/login fallback, PassNet enforcement, version/MSI flow, startup sequence (Splash -> Config -> License -> DB -> Login).
- EPIC 2 — Shell / MDI Application Framework: MDI shell, navigation (tree/outbar/toolbars), global theme/status bar, background workers (non-blocking UI).
- EPIC 3 — Customer Management: Search/create, duplicate detection, related entities overview, KYC/ID fields, segmentation.
- EPIC 4 — Loan Management: Create/edit/lock, review->approval->boarding, risk ratings/covenants/narratives, presentations, renewals/mods, LTV/DSCR/schedules.
- EPIC 5 — Collateral Management: Collateral registry, multi-loan relationships, appraisals/valuations, coverage rules/LTV validation.
- EPIC 6 — Deposit Management: Account lifecycle, transaction summary/history, imports/reconciliation, duplicate detection/error handling.
- EPIC 7 — Documentation Tracking (DT): Doc requirement templates, assignment/reassignment, exceptions/aging, enforcement on approval, evidence attachments/paths, bulk actions/waivers.
- EPIC 8 — Notes & Memos: Rich text notes, audit trails, visibility scope, soft delete/version behavior.
- EPIC 9 — Letters & Template Management: Template library/versioning, merge fields, batch/group generation, print/PDF/export.
- EPIC 10 — Reports & Dashboards: C1 FlexReports, parameterized reports, queueing long jobs, dashboard KPIs/filters, export formats (PDF/Excel/CSV).
- EPIC 11 — Follow-up Tasks & Notification: Reminder scheduling, task assignment, overdue tracking, email notifications (scheduler service).
- EPIC 12 — Financial Analysis (FA / Spread Module): Spread templates, ratio calculations, saving/loading analyses, conversion utilities.
- EPIC 13 — Board Reports (BR): Past Due/Non-Accrual/One-Obligor, report generation, BR DB connectivity.
- EPIC 14 — Board Report Scheduler / Windows Service: Automated schedule, job logging/retry, output retention policies, failure recovery.
- EPIC 15 — OCR Pipeline (ABBYY): Batch OCR processing, folder monitoring, error/retry handling, logging/audit.
- EPIC 16 — AI Tax Document Extraction (Azure Document Intelligence): Field extraction, XML mapping to codes, multipage/multi-occur, fallback to ABBYY, key security/rotation.
- EPIC 17 — ComplianceOne Integration: File exchange (IN/OUT paths), field mapping, error recovery/manual retry, version compatibility.
- EPIC 18 — Credit Bureau Integration: Request/response flows, status tracking, response parsing/masking, compliance handling, retries/downtime handling.
- EPIC 19 — Square1 Portal Integration: Portal connectivity, session management, role-based access.
- EPIC 20 — Mobile App TCP Integration: TCP listener (ports 5000–5100), message protocol, authentication/rate-limiting, logging/error handling.
- EPIC 21 — Global Configuration Management: INI + limited app.config, path validation, ports/timeouts/flags, admin-only access, audit of changes.
- EPIC 22 — Lookup Tables Management: CRUD for lookup codes, ordering/uniqueness, prevent deletion of in-use codes, bulk import/export.
- EPIC 23 — SMTP & Email System Configuration: SMTP host/SSL/TLS, test mode, credential protection, debug logging/transcripts.
- EPIC 24 — User, Roles, Permission Management: Role-based module access, user lifecycle (active/disabled), audit of role/permission changes.
- EPIC 25 — Data Access Layer & SQL Connectivity: SqlClient primary, OLE DB legacy handling, timeout rules, encrypted connections.
- EPIC 26 — Logging & Error Handling: Centralized error handler, Event Log integration, SMTP alerts, structured logging improvement backlog.
- EPIC 27 — Observability / Monitoring: Service health status, job failures/retries, AI/OCR failure tracking, DB connectivity metrics.
- EPIC 28 — File System & Temporary Data Housekeeping: OCR/AI temp purge, output retention, security ACL enforcement.
- EPIC 29 — Security & Privacy Controls: PII masking, secret management, encryption requirements, access control boundaries.
- EPIC 30 — Upgrade & Deployment Management: MSI installer paths, arch-specific handling (x64/x86), network backend support, rollback procedures, ST.Main.INI → Suntell.ini chain.
- EPIC 31 — Disaster Recovery & Backup Requirements: SQL backup expectations, configuration backup, service restart processes, change control.
- EPIC 32 — Performance & Capacity Management: Startup performance, search/report SLA, AI/OCR throughput, scheduler concurrency.
- EPIC 33 — Testing, QA & Acceptance Criteria: Functional/negative testing, integration tests, performance/regression tests, environment-specific smoke tests.
- EPIC 34 — Technical Debt & Migration Backlog: Migrate off OLE DB, secrets out of config files, refactor monolithic frmMDI, move to SqlClient everywhere, PackageReference modernization, structured logging enhancement.
- EPIC 35 — Third-Party Component Management: ComponentOne, TX Text Control, ABBYY, Azure Document Intelligence, GrapeCity Spread; licensing checks.

## Epic Stories

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

## Checklist Results Report 
### PM Checklist (Comprehensive Mode) 
 
**Executive Summary** 
- Overall PRD completeness: ~90% (Ready for architect with minor gaps) 
- MVP scope: Just Right (clear must-haves; out-of-scope noted in brief but not restated in PRD) 
- Readiness for architecture: Ready/Nearly Ready (needs minor clarifications below) 
- Top gaps: data requirements/migration not explicit; stakeholder/comms plan absent; architecture guidance light beyond constraints; UX flows not mapped, only goals. 
 
**Category Statuses** 
| Category                         | Status   | Critical Issues | 
| -------------------------------- | -------- | --------------- | 
| 1. Problem Definition & Context  | PASS     | None | 
| 2. MVP Scope Definition          | PARTIAL  | Out-of-scope not restated in PRD; MVP validation approach not explicit | 
| 3. User Experience Requirements  | PARTIAL  | No user journeys/flows; edge/error states not covered | 
| 4. Functional Requirements       | PASS     | None | 
| 5. Non-Functional Requirements   | PASS     | None | 
| 6. Epic & Story Structure        | PASS     | None | 
| 7. Technical Guidance            | PARTIAL  | Architecture guidance shallow (decisions/trade-offs not captured) | 
| 8. Cross-Functional Requirements | PARTIAL  | Data requirements/migration/retention specifics not captured | 
| 9. Clarity & Communication       | PARTIAL  | Stakeholder list and comms/approval plan not documented | 
 
**Top Issues by Priority** 
- BLOCKERS: None. 
- HIGH: Add data requirements (entities, retention, migration needs if any) to PRD; add UX flows/edge cases for primary journeys (startup/licensing, doc tracking, schedulers, OCR review, imports). 
- MEDIUM: Restate out-of-scope and MVP validation approach in PRD; add stakeholder list and comms/approval plan; add architecture guidance/trade-offs (e.g., logging/telemetry sink choices, MSI rollback strategy highlights). 
- LOW: Clarify performance baselines in PRD (reuse brief metrics) and add error-state handling notes in UI goals. 
 
**Recommendations**
- Add a short Out of Scope and MVP Validation Approach subsection referencing the brief.
- Add primary user journeys (licensing/startup, doc tracking/waiver, scheduler recovery, OCR exception review, imports) with edge/error handling.
- Capture data requirements: key entities, retention rules, any migration/backfill assumptions; align with NFR6 housekeeping.
- Document stakeholders and decision/approval path; add comms/update cadence.
- Extend technical guidance with explicit choices/trade-offs: telemetry sink(s), log schema/correlation ID pattern, MSI rollback steps, dependency validation process, and temp directory hygiene enforcement.

**Final Decision** 
- READY FOR ARCHITECT (with above clarifications to tighten scope and guidance). 
 
## Next Steps 
 
### UX Expert Prompt 
Using the attached PRD for ST Loan Management System (WinForms, .NET Framework 4.8), craft a UX plan that keeps familiar MDI/ribbon patterns, fast search/open, doc status/aging visibility, scheduler/licensing/health indicators, non-blocking jobs (reports/OCR/imports), notes with constrained rich text, and accessibility emphasis on keyboard/high-contrast/font scaling. Cover core screens listed in the PRD, status surfaces for schedulers, doc tracking board, OCR/AI review queue, and imports console. Propose interaction patterns and visual guardrails consistent with ComponentOne controls and existing branding. 
 
### Architect Prompt 
Using this PRD, propose an architecture for the WinForms/.NET Framework 4.8 LMS plus Windows services (Notification, Board Report Scheduler). Include: INI/app.config strategy with `[LMS] BACKEND`, arch-specific MSI paths (`MSI\\x64`/`MSI\\x86`), SQL Server + BR DB connectivity and encryption, ABBYY + Azure Document Intelligence integration with temp hygiene, dependency validation for ComponentOne/Spread/TX/Controls/Graphics DLLs, background workers for reports/notifications/OCR/imports, telemetry/health checks/alerts for licensing and schedulers, ports 5000-5100 for portal/TCP with auth/rate limits, and rollout/rollback guidance for version checks. Outline module boundaries, observability, and error taxonomy (IO/API/Parsing/Quota/Config/SQL). 









