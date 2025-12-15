# User Interface Design Goals 
 
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
 