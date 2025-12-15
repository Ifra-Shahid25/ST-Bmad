# EPIC 16 - AI Tax Document Extraction (Azure Document Intelligence)

### Story 16.1 AI Extraction with Fallback
User Story: As an analyst, I want AI tax extraction with fallback so that field mapping is accurate and resilient.
Acceptance:
- Extract fields and map to codes; support multipage/multi-occur; validate schema.
- Fallback to ABBYY on failure; retries/backoff for transient errors; track accuracy.
- Secure key handling; audit/telemetry with correlation IDs; no secrets in logs.
