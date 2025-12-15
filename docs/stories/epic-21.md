# EPIC 21 - Global Configuration Management

### Story 21.1 Config Admin and Audit
User Story: As an admin, I want safe configuration management so that paths/ports/timeouts/flags are governed.
Acceptance:
- Admin-only access to INI/app.config settings with validation; prevent invalid save; audit changes.
- Export/import config with masking of secrets; retain change history; rollbacks possible.
- Health check of config validity after changes with remediation guidance.
