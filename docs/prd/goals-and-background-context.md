# Goals and Background Context 
 
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