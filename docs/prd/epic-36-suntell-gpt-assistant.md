# EPIC 36: Suntell GPT Assistant - Brownfield Enhancement

## Epic Goal
Embed an Azure OpenAI-powered conversational assistant inside the Suntell WinForms MDI app to accelerate customer support tasks via natural language while keeping automations safe, auditable, and context-aware.

## Epic Description

**Existing System Context**
- Current relevant functionality: WinForms MDI shell with customer search, memos, and navigation modules.
- Technology stack: .NET WinForms, Azure OpenAI (gpt-4.1-nano), FlaUI for UI automation.
- Integration points: ChatWidgetForm hosted by frmMDI; automations target existing forms via AutomationId/Name; configuration-driven Azure endpoint/key.

**Enhancement Details**
- What's being added/changed: Embedded chat widget with conversational UI, structured JSON intent responses, optional automation links, and persistent chat history per session.
- How it integrates: ChatWidgetForm renders messages and invokes AzureOpenAI; intents route to FlaUI automations with confirmation gates; context tied to selected customer; offline mode shows AI-unavailable fallback.
- Success criteria: <=2s average assistant response, >=95% intent accuracy, 99.5% automation success, no impact to existing MDI workflows.

## Stories
1. Chat shell & Azure OpenAI integration — Build ChatWidgetForm UI, secure config for endpoint/deployment/key, handle request/response flow, render messages and errors.
2. Intent handling with safe FlaUI automation — Parse structured JSON, surface actionable links requiring confirmation for state changes, execute automations with success/failure logging.
3. Context persistence & resiliency — Persist chat history per user session, rehydrate on restart, tie context to selected customer, provide AI-unavailable/offline messaging.

## Compatibility Requirements
- [ ] MDI navigation and host form lifecycle remain unchanged.
- [ ] No external API or database schema changes; configuration-only wiring.
- [ ] UI matches existing WinForms patterns (header drag, FlowLayoutPanel chat, Enter-to-send).
- [ ] Performance stays asynchronous/non-blocking with ~2s average response target.

## Risk Mitigation
- Primary Risk: Automations triggering on the wrong target/context.
- Mitigation: Confirmation required for state-changing actions; validate AutomationId/Name and selected customer before execution; abort and log on mismatch.
- Rollback Plan: Config flag to disable assistant/automations; remove chat control from frmMDI; revert to manual navigation.

## Definition of Done
- [ ] All three stories completed with acceptance criteria met.
- [ ] Assistant degrades gracefully when Azure/OpenAI is unavailable; offline notice displayed.
- [ ] Automation telemetry captures intents, latency, and errors without PII; logs available for audit.
- [ ] Documentation updated (config, user guidance), and existing functionality smoke-tested to confirm no regression.

## Validation Checklist
- [ ] Scope fits within 1-3 stories and follows existing patterns.
- [ ] Risk to existing system is low with feasible rollback.
- [ ] Success criteria and integration points are measurable and identified.
- [ ] Dependencies and verification of existing functionality are covered in testing.

## Story Manager Handoff
"Please develop detailed user stories for this brownfield epic. Key considerations:
- This is an enhancement to an existing WinForms MDI system using Azure OpenAI (gpt-4.1-nano) and FlaUI.
- Integration points: ChatWidgetForm hosted in frmMDI; automations target existing forms via AutomationId/Name with customer context.
- Existing patterns to follow: current MDI UI layout, async/non-blocking calls, config-driven secrets (no hardcoded keys).
- Critical compatibility requirements: no API/DB changes, minimal performance impact, confirmation for state changes, audit-friendly logging.
- Each story must include verification that existing functionality remains intact."
