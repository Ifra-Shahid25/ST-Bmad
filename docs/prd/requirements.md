# Requirements 
 
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
 