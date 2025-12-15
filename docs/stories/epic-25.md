# EPIC 25 - Data Access Layer & SQL Connectivity

### Story 25.1 SqlClient-First Data Layer
User Story: As a platform engineer, I want standardized SQL connectivity so that data access is reliable and secure.
Acceptance:
- Standardize on SqlClient with timeouts and encrypted connections; handle legacy OLE DB safely.
- Centralize connection management; retry/backoff patterns defined; telemetry on DB failures.
- No breaking changes to existing APIs; masking for sensitive data in logs.
