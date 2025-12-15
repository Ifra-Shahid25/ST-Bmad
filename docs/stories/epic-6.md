# EPIC 6 - Deposit Management

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
