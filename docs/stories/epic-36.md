# EPIC 36 - Suntell GPT Assistant

### Story 36.1 Chat Shell and Azure OpenAI Integration
User Story: As a support rep, I want an embedded chat shell that talks to Azure OpenAI so that I can get quick help without leaving the MDI app.
Acceptance:
- ChatWidgetForm hosted inside frmMDI with header drag, FlowLayoutPanel transcript, and input bar with Enter-to-send; resizes with MDI layout and does not interfere with existing window lifecycle.
- Config-driven Azure settings (endpoint, deployment/model, API key) loaded from config/INI; no hardcoded secrets; validation errors surfaced with user-friendly guidance.
- Request pipeline uses async calls with last 6-message context and targets <=2s average response; displays bot/human messages, inline errors, and prevents duplicate sends while in flight.
- Graceful handling for network/429/timeout/unavailable responses; shows AI unavailable banner and disables automation affordances when backend is down.
- Telemetry captures intent request metadata (no PII), latency, and failures using existing logging pattern.

### Story 36.2 Intent Handling with Safe FlaUI Automation
User Story: As a support rep, I want the assistant to propose safe automations so that I can navigate and update the app faster without unintended changes.
Acceptance:
- Parse structured JSON responses to extract intent name, parameters, and automation steps; ignore or strip unknown or malformed fields safely.
- Surface automation CTA only when intent is actionable; state-changing actions require explicit confirmation; read-only intents may run directly per safety rules.
- Validate selected customer/context and target form AutomationId/Name before executing; abort with guidance on mismatch or missing elements.
- Execute FlaUI automation asynchronously with success/failure status, logs, and remediation hints; failures avoid partial writes and leave the UI responsive.
- Automation events recorded via existing telemetry/logging (no PII), including intent, outcome, latency, and error details.

### Story 36.3 Context Persistence and Resiliency
User Story: As a support rep, I want chat context and customer alignment to persist so that I can resume conversations and automations reliably.
Acceptance:
- Persist chat history per user session (recent messages) to disk or configured storage; exclude secrets and enforce rotation/size limits.
- On restart, rehydrate conversation and restore assistant state; tie context to the currently selected customer and prompt to reselect if mismatched.
- Provide explicit AI unavailable/offline state when Azure/OpenAI cannot be reached; hide or disable automation CTAs while offline.
- Ensure history and telemetry handling respect PII rules; no customer-sensitive data stored in plain text logs.
- Persistence and offline flows are non-blocking and do not break existing MDI navigation or module loading.
