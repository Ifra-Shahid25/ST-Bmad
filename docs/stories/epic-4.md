# EPIC 4 - Loan Management

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
