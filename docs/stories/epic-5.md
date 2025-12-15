# EPIC 5 - Collateral Management

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
