# Epic List

## EPIC 1: Authentication, Licensing & Startup Pipeline
SSO/login fallback; PassNet enforcement; version/MSI flow; startup sequence (Splash -> Config -> License -> DB -> Login).

## EPIC 2: Shell / MDI Application Framework
MDI shell; navigation (tree/outbar/toolbars); global theme/status bar; background workers (non-blocking UI).

## EPIC 3: Customer Management
Search/create; duplicate detection; related entities overview; KYC/ID fields; segmentation.

## EPIC 4: Loan Management
Create/edit/lock; review -> approval -> boarding; risk ratings/covenants/narratives; presentations; renewals/mods; LTV/DSCR/schedules.

## EPIC 5: Collateral Management
Collateral registry; multi-loan relationships; appraisals/valuations; coverage rules/LTV validation.

## EPIC 6: Deposit Management
Account lifecycle; transaction summary/history; imports/reconciliation; duplicate detection/error handling.

## EPIC 7: Documentation Tracking (DT)
Doc requirement templates; assignment/reassignment; exceptions/aging; enforcement on approval; evidence attachments/paths; bulk actions/waivers.

## EPIC 8: Notes & Memos
Rich text notes; audit trails; visibility scope; soft delete/version behavior.

## EPIC 9: Letters & Template Management
Template library/versioning; merge fields; batch/group generation; print/PDF/export.

## EPIC 10: Reports & Dashboards
C1 FlexReports; parameterized reports; queueing long jobs; dashboard KPIs/filters; export formats (PDF/Excel/CSV).

## EPIC 11: Follow-up Tasks & Notification
Reminder scheduling; task assignment; overdue tracking; email notifications (scheduler service).

## EPIC 12: Financial Analysis (FA / Spread Module)
Spread templates; ratio calculations; saving/loading analyses; conversion utilities.

## EPIC 13: Board Reports (BR)
Past Due/Non-Accrual/One-Obligor; report generation; BR DB connectivity.

## EPIC 14: Board Report Scheduler / Windows Service
Automated schedule; job logging/retry; output retention policies; failure recovery.

## EPIC 15: OCR Pipeline (ABBYY)
Batch OCR processing; folder monitoring; error/retry handling; logging/audit.

## EPIC 16: AI Tax Document Extraction (Azure Document Intelligence)
Field extraction; XML mapping to codes; multipage/multi-occur; fallback to ABBYY; key security/rotation.

## EPIC 17: ComplianceOne Integration
File exchange (IN/OUT paths); field mapping; error recovery/manual retry; version compatibility.

## EPIC 18: Credit Bureau Integration
Request/response flows; status tracking; response parsing/masking; compliance handling; retries/downtime handling.

## EPIC 19: Square1 Portal Integration
Portal connectivity; session management; role-based access.

## EPIC 20: Mobile App TCP Integration
TCP listener (ports 5000-5100); message protocol; authentication/rate-limiting; logging/error handling.

## EPIC 21: Global Configuration Management
INI plus limited app.config; path validation; ports/timeouts/flags; admin-only access; audit of changes.

## EPIC 22: Lookup Tables Management
CRUD for lookup codes; ordering/uniqueness; prevent deletion of in-use codes; bulk import/export.

## EPIC 23: SMTP & Email System Configuration
SMTP host/SSL/TLS; test mode; credential protection; debug logging/transcripts.

## EPIC 24: User, Roles, Permission Management
Role-based module access; user lifecycle (active/disabled); audit of role/permission changes.

## EPIC 25: Data Access Layer & SQL Connectivity
SqlClient primary; OLE DB legacy handling; timeout rules; encrypted connections.

## EPIC 26: Logging & Error Handling
Centralized error handler; Event Log integration; SMTP alerts; structured logging improvement backlog.

## EPIC 27: Observability / Monitoring
Service health status; job failures/retries; AI/OCR failure tracking; DB connectivity metrics.

## EPIC 28: File System & Temporary Data Housekeeping
OCR/AI temp purge; output retention; security ACL enforcement.

## EPIC 29: Security & Privacy Controls
PII masking; secret management; encryption requirements; access control boundaries.

## EPIC 30: Upgrade & Deployment Management
MSI installer paths; arch-specific handling (x64/x86); network backend support; rollback procedures; ST.Main.INI -> Suntell.ini chain.

## EPIC 31: Disaster Recovery & Backup Requirements
SQL backup expectations; configuration backup; service restart processes; change control.

## EPIC 32: Performance & Capacity Management
Startup performance; search/report SLA; AI/OCR throughput; scheduler concurrency.

## EPIC 33: Testing, QA & Acceptance Criteria
Functional/negative testing; integration tests; performance/regression tests; environment-specific smoke tests.

## EPIC 34: Technical Debt & Migration Backlog
Migrate off OLE DB; secrets out of config files; refactor monolithic frmMDI; move to SqlClient everywhere; PackageReference modernization; structured logging enhancement.

## EPIC 35: Third-Party Component Management
ComponentOne; TX Text Control; ABBYY; Azure Document Intelligence; GrapeCity Spread; licensing checks.


## EPIC 36: Suntell GPT Assistant
Embedded Azure OpenAI chat assistant in WinForms MDI with safe FlaUI automations, contextual customer awareness, and offline/fallback handling.
