# EPIC 1 - Authentication, Licensing & Startup Pipeline

### Story 1.1 Licensing/SSO Gate and Startup
User Story: As an operations admin, I want startup licensing and SSO gating so that only authorized users can open modules.
Acceptance:
- Block startup and module entry when PassNet/SSO/license validation fails; show remediation guidance and audit outcome.
- Enforce per-module license flags and hide/deny unauthorized modules; log attempts with correlation IDs.
- Telemetry captures auth/config/network errors; flows are non-blocking and retry-safe.

### Story 1.2 MSI/Version Preflight and Rollback
User Story: As a desktop engineer, I want MSI/version and dependency preflight so that upgrades do not break the shell.
Acceptance:
- Detect arch mismatch and missing MSI/DLLs (ComponentOne/Spread/TX/controls) and block with actionable guidance.
- Provide rollback path and record version/build info in audit/telemetry.
- Preflight runs without freezing UI and produces structured status (pass/warn/fail).
