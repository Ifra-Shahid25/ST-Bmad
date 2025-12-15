# Project Brief: ST Loan Management System (ST Main)

## Executive Summary
- Windows desktop Loan Management System (LMS) for lenders, credit teams, operations, and compliance to manage customers, loans, collateral, documentation, reports, and scheduled notifications/board reports.
- Solves fragmented loan operations, compliance evidence, and reporting by centralizing workflows with licensing/feature gating and auditable data on SQL Server.
- Targets mid-size financial institutions needing reliable, on-premise WinForms workflows with OCR/AI extraction for documents and integrations (Credit Bureau, ComplianceOne, Square1 Portal, mobile TCP).
- Value: faster processing with fewer exceptions, reliable schedulers, clearer audit trails, and reduced operational risk while staying on .NET Framework 4.8/WinForms.

## Problem Statement
- Current state: complex WinForms app with many modules (customers, loans, docs, reports, schedulers) and multiple services/INIs; doc tracking and scheduler reliability are critical pain points.
- Impact: operational risk from missing/late documentation, slow reporting, and license/config misalignment; manual recovery when schedulers fail; onboarding and updates can stall due to config/version issues.
- Observability gaps: limited health checks and telemetry for schedulers/licensing cause delayed detection and manual triage during incidents.
- Gaps in existing solutions: generic LMS tools lack tailored PassNet licensing, ABBYY/Azure AI extraction mapping, and board-report scheduling needs; cloud rewrites are out of scope.
- Urgency: maintain reliability, compliance, and auditability now while enabling incremental modernization without breaking WinForms/.NET 4.8 constraints.

## Proposed Solution
- Maintain and enhance the on-prem WinForms LMS with centralized customer/loan/collateral workflows, robust documentation tracking, and auditable notes/memos.
- Enforce PassNet licensing and authentication up front; keep services (Notification, Board Report Scheduler) resilient with retries/backoff and clear status.
- Add preflight/config diagnostics (paths, ports, licensing assets, third-party DLLs) plus telemetry/alerting for schedulers and licensing checks to shorten MTTR.
- Integrate ABBYY OCR and Azure Document Intelligence for tax-form extraction; map outputs to internal codes with secure key handling and temp file hygiene.
- Provide configurable reports/dashboards (C1 FlexReport), deposits, letters via TX Text Control, and integrations (Credit Bureau, ComplianceOne, Square1 Portal, mobile TCP) with role-based access and background workers.
- Deliver Financial Analysis module with spread templates, ratio calculations, validated data mapping, versioned spreads, and export of analysis results.
- Provide import tooling (LMSImport) with CSV/Excel schema validation, duplicate detection/idempotency, error reporting, and dry-run capability.
- Support CustomTemplates for UI/report templates with validation, version control, and role-based publishing; ensure internal controls/graphics libraries and DLL dependencies are present at runtime.

## Target Users
### Primary User Segment: Loan Operations & Credit Teams
- Loan officers, credit analysts, documentation/exception specialists, branch staff, portfolio managers needing fast customer/loan creation, collateral linkage, doc tracking, notes/memos, reports, and follow-ups with licensing enforced.

### Secondary User Segment: Compliance, Executive Reporting, IT/Ops
- Compliance/risk officers, auditors, and board/executive reporting users focused on audit trails, scheduled board reports, and secure exports.
- IT/operations managing installs/updates, INI/configuration, scheduler services, backups, licensing assets, and monitoring.
- Mobile/portal users accessing TCP/portal endpoints for limited workflows; require secure, reliable connectivity.

## Goals & Success Metrics
### Business Objectives
- Reduce documentation exceptions and overdue items (target: <10% exception rate; baseline to confirm).
- Improve loan onboarding throughput and data accuracy (target: 20% faster end-to-end flow vs current baseline; near-term goal: create <2 minutes with required fields).
- Increase reliability of scheduled notifications and board reports (target: 99.5%+ weekly success with retries; MTTR <30 minutes).
- Ensure licensing/compliance enforcement before feature access (target: 100% gating with auditable logs; SSO/license check success >99%).

### User Success Metrics
- Time to create/search/open customer/loan records (target: search/open <2s; create <2 minutes).
- Documentation closure time and aging distribution (target: reduce >30-day aged items by 30%).
- Report/board report success rate and latency (target: >99% success; runtime <2 minutes for standard reports).
- Notification delivery success rate and retry recovery time (target: >99% delivery with recovery within 10 minutes of failure).
- OCR/AI extraction accuracy for tax forms (target: mapped field accuracy >95% with manual review queue for exceptions).

### Key Performance Indicators (KPIs)
- % documentation items on time; exception rate trend (target: <10% exceptions; trending down QoQ).
- Avg search/open latency; splash-to-shell startup under target (target: <5s cold start on supported hardware).
- Scheduler success rate; mean time to detect/recover failures (target: detection <5 minutes via telemetry; recovery <30 minutes).
- License check/SSO success rate; update prompt compliance (target: >99% success; >90% of users on current MSI within 30 days).
- OCR/AI extraction throughput and accuracy (target: 95%+ accuracy; processing <60s per batch).

## MVP Scope
### Core Features (Must Have)
- Authentication/SSO with licensing and feature gating on startup and module entry.
- Customers/Loans/Collateral management with validations, narratives, and audit trails.
- Documentation Tracking: assignments, exceptions, reassignment, status/aging, waiver with reason.
- Notes/Memos with author/timestamp; Follow-ups/Tasks with notifications and due dates; rich text rules, visibility/permissions, soft-delete with audit log.
- Reports & Dashboards via C1 FlexReport; Board Reports with scheduler service against BR DB.
- Notification scheduler service with retries/backoff and status logging.
- Health checks/telemetry for schedulers/licensing with basic alerting and log surfacing for ops.
- Deposits: account views, balances, transaction history, and imports/reconciliation with validation.
- Letters/Templates via TX Text Control with merge/print/export flows.
- Financial Analysis (FA): spread templates, ratio calculations, validated data mapping, saved/exported analyses, and versioned spreads.
- LMSImport: CSV/Excel schema validation, duplicate detection/idempotency, error reporting, and dry-run mode.
- CustomTemplates: custom UI/report templates with file validation, version control, and role-based access/publishing.
- Controls/LAControls/Graphics runtime dependencies (images/icons/fonts) validated and present.
- Integrations: Credit Bureau requests, ComplianceOne file exchange, Square1 Portal access, mobile TCP server (ports 5000-5100).
- OCR/AI extraction: ABBYY OCR and Azure Document Intelligence for tax forms with XML mapping, multi-occurrence table handling, page/size limits, temp file cleanup, mapping rules to internal codes, error taxonomy (IO/API/Parsing/Quota), and fallback-to-ABBYY logic.
- UDLMS_Net/mobile TCP: authenticated connections, rate limiting, defined message formats/protocol, connection monitoring/logging, and security constraints.
- Background workers/queues for long-running jobs (reports, notifications, AI/OCR) to avoid UI blocking.
- Audit trail coverage for key entities (loans, docs/waivers, notes/memos, follow-ups) with user/timestamp/old-new values and prohibited deletes where required.
- Configuration UI for paths, timeouts, ports, feature flags; dual connection strings (LMS DB, BR DB).
- Version check/MSI prompt flow with arch-specific paths; install/update guidance.

### Out of Scope for MVP
- Non-Windows clients, cloud-native rewrite, or migration beyond .NET Framework 4.8/WinForms.
- Pixel-level UX redesign; PackageReference migration; broad architectural refactor.

### MVP Success Criteria
- All core modules functional with licensing enforced; startup/login path stable.
- Documentation tracking and schedulers operate with logged status, alerting, and recovery steps.
- Reports/board reports and notifications complete without blocking UI; background tasks stable.
- Configurable paths/ports/credentials validated via preflight; secrets not stored in plaintext.
- Telemetry available for schedulers/licensing outcomes with MTTR targets reachable.
- Version check/update flow honors arch detection (x64/x86), blocks mismatched clients appropriately, and provides rollback steps.
- Data retention and housekeeping: temp OCR/AI directories cleaned, logs rotated per policy, and report/notification outputs retained per agreed durations.
- Audit trails enforced for key entities (loans, docs/waivers, notes/memos, follow-ups) with user/timestamp/old-new values; prohibited deletes honored.

## Post-MVP Vision
### Phase 2 Features
- Enhanced dashboards/analytics with better caching and drill-down.
- Improved doc mapping/validation for AI extraction; richer exception workflows.
- More resilient scheduler telemetry and alerting; sandboxed dry-run tools and replay testing for schedulers.
- Guided installer/upgrade automation with rollback paths and checksum/license validation.

### Long-term Vision
- Incremental decoupling of services; clearer module boundaries for maintainability.
- Progressive hardening of security (encryption defaults, stricter masking) and observability (correlation IDs, rotation).
- Optional web/portal enhancements while keeping WinForms core stable.

### Expansion Opportunities
- Additional bureau/compliance integrations; template marketplace for letters/reports.
- Performance tuning playbooks; automated config validation and health checks.

## Technical Considerations
### Platform Requirements
- Target Platforms: Windows desktop WinForms (.NET Framework 4.8) with MDI shell.
- Browser/OS Support: Windows only; ensure required third-party DLLs available at runtime.
- Performance Requirements: Splash-to-shell under ~5s on supported hardware; avoid UI blocking; background workers for long tasks.

### Technology Preferences
- Frontend: WinForms with ComponentOne controls/FontAwesome icons.
- Backend: C# .NET Framework 4.8 with `packages.config`; background workers for schedulers and long tasks.
- Database: SQL Server (primary LMS DB) plus separate Board Reports DB; prefer SqlClient over OLE DB.
- Hosting/Infrastructure: Windows clients/services; INI-driven configuration; secure storage for keys/credentials; MSI-based deployment with arch-specific DLL directories.

### Architecture Considerations
- Repository Structure: existing modules (Util, Data, Error, Customers, Loans, Collateral, DT, Reports, Dashboards, FollowUp, Configure, Lookup, FA, BR/BRSchedule, Credit Bureau, OCR/AI, Portal, TCP).
- Service Architecture: Windows services for Notification and Board Report scheduling; test harness (BRTestGen) isolated from production; NotificationTester for safe SMTP tests.
- Integration Requirements: ABBYY OCR paths, Azure Document Intelligence endpoint/key, ComplianceOne file exchange, Credit Bureau APIs, Square1 Portal, TCP server ports, mobile TCP server ports (5000-5100).
- Security/Compliance: PassNet licensing enforcement; encrypted SQL where possible; mask PII in UI/logs; secure temp directories and keys; clarify SSN/TIN masking and export rules.
- Additional Components: Deposits module, Letters/Templates, LMSImport, ConfigSMTP, CustomTemplates, Controls/LAControls/Graphics, Spread/ComponentOne/TX Text Control DLLs; ensure runtime licenses and versions present.
- Letters/Templates: template merge and batch generation, versioning/publishing controls, and print/PDF export flows.
- Notes/Memos: rich text formatting constraints, visibility/permissions, soft-delete with audit, and export rules if present.
- Financial Analysis: spread templates, ratio calculations, validated mapping to data sources, saved/exported analyses, and versioned spreads.
- LMSImport: CSV/Excel schema validation, duplicate detection/idempotency, error reporting, and dry-run execution.
- CustomTemplates: file validation, version control, role-based access, and publishing workflow for custom UI/report templates.
- Controls/LAControls/Graphics: internal WinForms control libraries with image/icon dependencies; validate runtime resource availability.
- UDLMS_Net/mobile TCP: authentication model, rate limiting, message formats/protocol, connection monitoring/logging, and required security constraints.
- Board Reports: separate BR SQL DB; scheduler retries/logging; output rotation policies; BRTestGen for dry runs; parameter validation and collision handling.
- Version check/MSI flow: architecture detection (x64/x86), MSI folder structure (`MSI\\x64`/`MSI\\x86`), mismatch behavior/update blocking, rollback guidance, and local vs UNC backend handling.
- Background workers/queues: non-blocking UI rules; job queue behavior for reports/notifications/AI-OCR with retries/backoff.
- Logging/Observability: Event Log usage, scheduler health monitoring, failure thresholds, telemetry signals/SLO expectations, and log rotation/retention policies.
- Security hardening: remove AI keys from app.config; secure storage for all secrets; encryption-at-rest guidance; certificate requirements for SQL encryption; stricter masking for SSN/TIN and sensitive logs.
- Audit trails: capture user/timestamp/old-new values for loans, docs/waivers, notes/memos, follow-ups; prohibit unauthorized edits/deletes.
- Data retention & housekeeping: temp directory cleanup (OCR/AI), log rotation, notification/board report retention policies.
- Deployment/DR: required DLL validation, backup/recovery expectations, version rollback procedures, and service restart runbooks.
- Startup sequence: splash → config load → license check → DB check → version check → SSO/login → MDI load.
- External component licensing: ABBYY, ComponentOne, TX Text Control, GrapeCity Spread runtime license validation and deployment of required DLLs.

## Constraints & Assumptions
### Constraints
- **Budget:** Not provided; assume maintenance/stabilization budget with targeted investments; confirm capex/opex limits.
- **Timeline:** Prioritize near-term reliability and compliance; major rewrites deferred.
- **Resources:** Existing engineering/ops teams manage Windows services and INI/config updates; likely limited dedicated QA; vendors provide licensing keys/DLLs.
- **Technical:** Remain on .NET Framework 4.8/WinForms with `packages.config`; dual DB connections; on-prem Windows (likely 64-bit) with arch-specific DLL paths; INI-driven configuration; no cloud rewrite.

### Key Assumptions
- SQL Server and BR DB reachable with provided connection strings; encryption preferred.
- Licensing assets and third-party DLLs available at runtime; temp/output directories writable and secured.
- Feature flags/INI paths kept current per environment; environment-specific MSI shares exist for updates; service accounts have required permissions.
- Supported OS is Windows 10/11 (64-bit) with reliable LAN connectivity; offline/air-gapped constraints accommodated via licensing assets.
- INI chain uses `ST.Main.INI` -> `Suntell.ini` with `[LMS] BACKEND` hosting MSI folders (`MSI\\x64`/`MSI\\x86`); adjust to UNC backend if not local.
- MSI prompt uses arch-specific path; both `x64` and `x86` packages exist or prompts are gated appropriately.
- Service display names (e.g., Suntell Notification Service, Suntell Data Aggregation Service) remain consistent across environments for restart/monitoring scripts.
- INI keys: `[LMS] BACKEND` defines base share for MSI/INI/docs; `SUNINI` points to `Suntell.ini`; OCR/ComplianceOne paths set in INI; environment-specific path rules documented for local vs UNC backends.

## Risks & Open Questions
### Key Risks
- Third-party licensing or key expiry (ComponentOne, TX Text Control, ABBYY, Azure AI) causing runtime failures.
- Scheduler reliability or duplicate runs leading to missed/duplicated notifications/reports.
- Document mapping accuracy for AI/OCR; fallback/cleanup failures causing data gaps or PII exposure.
- Configuration drift across INI/app.config leading to connection or path failures.
- Limited telemetry/alerting delaying detection of scheduler/licensing failures, increasing MTTR.
- MSI/update or arch mismatch (32/64-bit) causing missing DLLs or service crashes.
- INI/BACKEND path misconfiguration or missing MSI share causing failed version checks/prompts.
- Service account permissions insufficient for Event Log, shares, or SMTP, causing silent failures.
- TCP port conflicts (5000-5100) impacting mobile/portal connectivity.
- Credit Bureau/ComplianceOne data handling risk if retention/masking rules are unclear.
- Bureau downtime or slow responses causing backlogs; need retries/backoff and user messaging.
- ComplianceOne partial file recovery or path issues leading to stuck transfers.
- DT bulk waiver rollback requirements if erroneous waivers are applied.
- Dashboard refresh/caching rules causing stale data or performance regressions.

### Open Questions
- Target service levels (uptime, latency) for schedulers, searches, and report generation?
- Role-based access specifics for sensitive reports and fields (SSN/TIN masking, exports)?
- Data retention and purging policies for temp OCR/AI outputs and bureau responses?
- Exact licensing/product flags required per module in different environments?
- Supported Windows versions and architecture expectations (32/64-bit) for clients and services?
- How offline/air-gapped environments handle license validation, updates, and telemetry?
- Are MSI shares local (`C:\\Program Files (x86)\\Suntell\\MSI\\<ENV>\\`) or UNC (`\\\\fileserver\\ST\\backend\\MSI\\<ENV>\\`), and who maintains them?
- Do service names vary by environment (prefixes/suffixes) or remain standard for automation?

### Areas Needing Further Research
- Performance baselines for splash-to-shell, search latency, and report runtimes on supported hardware.
- Security posture review (encryption defaults, secret storage, PII handling in logs/exports).
- Detailed mapping tables for AI extraction to internal codes and validation coverage.
- Operational runbooks for scheduler recovery, MSI rollback per environment, and license renewal.
- Telemetry/alerting coverage for services (Notification, Board Report Scheduler, licensing) and thresholds for SLOs.
- Deposits, Letters/Templates, LMSImport, ConfigSMTP, CustomTemplates module behaviors and validation rules to ensure parity with existing implementations.

## Appendices
### A. Research Summary
- Derived from `general requirement.md` (codebase analysis of ST Loan Management System, modules, integrations, and ops guidance). No separate user research or competitor analysis provided yet.

### B. Stakeholder Input
- Pending stakeholder interviews (loan officers, compliance, IT/ops, exec reporting).

### C. References
- `general requirement.md`

## Next Steps
### Immediate Actions
1. Define telemetry/alerting plan for schedulers, notifications, and licensing (detection <5 minutes, MTTR <30 minutes); choose signals, thresholds, and sinks.
2. Build install/update verification checklist (MSI shares, arch paths, service account rights) and rollback steps; confirm 32/64-bit DLL sets.
3. Capture OCR/AI mapping validation process and create exception handling workflow for manual review; set accuracy thresholds and reprocessing steps.
4. Validate environment assumptions: INI paths, DB connectivity (LMS + BR), licensing assets, third-party DLL presence (arch-specific).
5. Confirm target service levels and security/retention policies with compliance/ops; set baseline metrics.
6. Align module priorities for MVP vs Phase 2 (docs tracking, schedulers, AI/OCR robustness).
7. Draft migration/hardening checklist for secrets, logging, temp directory hygiene, and PII masking/export rules.

### PM Handoff
This Project Brief provides the full context for ST Loan Management System (ST Main). Please start in 'PRD Generation Mode', review the brief thoroughly to work with the user to create the PRD section by section as the template indicates, asking for any necessary clarification or suggesting improvements.
