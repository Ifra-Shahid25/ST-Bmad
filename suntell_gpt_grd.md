# 🧠 Suntell GPT Assistant – General Requirements Document

## 1. Overview
The **Suntell GPT Assistant** is an integrated AI chat system built for the **Suntell WinForms application**.
It provides intelligent automation, customer search, and natural conversational support — powered by **Azure OpenAI**.
The goal is to **augment the existing MDI interface** by embedding a conversational assistant that can understand user intent, run automations, and maintain contextual memory.

---

## 2. Core Objectives
1. **Conversational Interface:** Allow users to communicate naturally with the system.
2. **Actionable Intelligence:** Detect intent and execute UI automation tasks.
3. **Integration with MDI App:** Link chat-driven actions with existing modules.
4. **Security:** Protect API keys and sensitive data via configuration.
5. **Persistence:** Maintain chat history and rehydrate sessions on restart.

### 2.1 Scope
#### In Scope
- Embedded AI chat widget within Suntell WinForms MDI application
- Customer search, memo access, and system navigation via chat
- UI automation using FlaUI
- Context-aware conversations tied to selected customer
- Persistent chat history per user session

#### Out of Scope
- Voice-based interactions
- External CRM data modification
- Autonomous actions without user confirmation
- LLM training or fine-tuning
- Mobile or web UI support

---

## 3. System Architecture

### 3.1 Major Components
| Component | Description |
|------------|--------------|
| **ChatWidgetForm.cs** | Core UI component handling chat input/output, history, and Azure OpenAI integration. |
| **frmMDI.cs** | Main host form managing customer selection, chat widget lifecycle, and MDI context. |
| **AzureOpenAI Integration** | Handles LLM prompts, structured JSON parsing, and intent routing. |
| **FlaUI Automation** | Executes user commands on the WinForms UI. |

---

## 4. GPT Model Configuration

| Setting | Description |
|----------|--------------|
| Provider | Azure OpenAI |
| Deployment | gpt-4.1-nano |
| Max Tokens | 800 |
| Temperature | 0.2 |
| Context Window | Last 6 messages |

---

## 5. Behavior and Interaction

### 5.1 User Flow
1. User enters message
2. AzureCall() invoked
3. Model returns structured JSON
4. Message rendered in UI
5. Automation link shown if applicable
6. User confirms → automation executes

### 5.2 Safety & Confirmation Rules
- Confirmation required for state-changing actions
- Read-only actions may execute directly
- Never guess customer identity

---

## 6. Automation Execution
- Implemented via FlaUI
- Uses AutomationId with fallback by Name
- Returns success/failure with logs

---

## 7. UI Design
- Header with drag
- FlowLayoutPanel chat area
- Input bar with Enter-to-send
- Responsive resizing

---

## 8. Configuration & Security

### 8.1 App Configuration
- Azure endpoint, deployment, API key via config
- No hardcoded secrets

### 8.2 Non-Functional Requirements
- Avg response ≤ 2s
- Async UI only
- 99.5% automation success

### 8.3 Offline / Degraded Mode
- Show AI unavailable message
- Disable automations
- Manual UI still usable

---

## 9. Logging & Telemetry
- Intent detection
- Automation triggers
- Latency & errors
- No PII storage

---

## 10. Acceptance Criteria
- Smooth UI rendering
- ≥95% intent accuracy
- Correct automation
- History persistence

---

## 11. Future Enhancements
- More intents
- Telemetry dashboards
- Multilingual support
- Newer GPT models

---

## 12. Appendix

### Assumptions
- Authenticated users
- Stable AutomationIds

### Constraints
- WinForms only
- No background services

### Glossary
| Term | Meaning |
|------|--------|
| Intent | Parsed user intention |
| Automation | FlaUI UI action |
| Context | Customer + chat history |

