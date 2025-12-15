# EPIC 26 - Logging & Error Handling

### Story 26.1 Centralized Error Handling
User Story: As an engineer, I want centralized error handling so that failures are captured consistently.
Acceptance:
- Central error handler with Event Log integration and optional SMTP alerts; structured logging schema with correlation IDs.
- Error taxonomy applied across app/services; retention/rotation defined; debug logging safe for secrets.
- Validation that logs avoid PII unless masked; audit access to sensitive logs.
