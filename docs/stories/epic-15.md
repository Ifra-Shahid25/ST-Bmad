# EPIC 15 - OCR Pipeline (ABBYY)

### Story 15.1 ABBYY Batch OCR
User Story: As an imaging operator, I want ABBYY batch OCR with monitoring so that documents process reliably.
Acceptance:
- Folder monitoring with input validation; batch processing off UI thread.
- Error/retry handling with taxonomy; audit/log outcomes; retries bounded.
- Temp hygiene (secure/writable; cleanup after processing); masking for sensitive data.
