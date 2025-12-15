# Data Model Overview 
- Core entities: customers, loans, collateral, documentation items, waivers, notes/memos, follow-ups/tasks, users/roles, reports/board reports, imports, OCR/AI runs, audit logs. 
- Relationships: customers ↔ loans (1:N), loans ↔ collateral (1:N), loans/customers ↔ documentation items (1:N), documentation ↔ waivers (0:1), customers/loans ↔ notes/follow-ups (1:N), scheduler jobs ↔ report outputs (1:N), imports ↔ imported records (1:N with idempotency keys). 
- Sensitive fields: SSN/TIN, PII in notes/exports; must be masked in UI/logs/exports. 
- Identifiers: stable IDs for customers/loans/docs; idempotency keys for imports; correlation IDs for background jobs. 
- Audit scope: create/edit/status/waiver changes across docs/loans/collateral/notes/follow-ups; access to sensitive exports logged. 
