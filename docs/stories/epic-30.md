# EPIC 30 - Upgrade & Deployment Management

### Story 30.1 MSI Deployment and Rollback
User Story: As a release manager, I want controlled MSI deployment so that upgrades are safe and reversible.
Acceptance:
- MSI installer paths support x64/x86 with network backend; version check/prompt flow with rollback steps.
- Environment chain (ST.Main.INI -> Suntell.ini) validated; preflight upgrade checks logged.
- Audit upgrade/rollback actions; failure guidance provided.
