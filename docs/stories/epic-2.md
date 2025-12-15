# EPIC 2 - Shell / MDI Application Framework

### Story 2.1 MDI Shell and Navigation
User Story: As a user, I want a themed MDI shell with navigation so that I can open modules and status surfaces predictably.
Acceptance:
- Navigation (tree/outbar/toolbars) and status bar respect permissions; unauthorized modules hidden/blocked.
- Windows open/restore/close reliably with remembered layout; no leaks or orphaned child windows.
- Theming aligns with ComponentOne styles; shell remains responsive while loading modules.

### Story 2.2 Background Worker UX
User Story: As a user, I want long-running UI actions to run in the background so that the shell stays responsive.
Acceptance:
- Long jobs use background worker patterns with progress/status surfaces; no UI thread blocking.
- Duplicate/overlapping runs prevented; safe cancellation where applicable with user guidance.
- Telemetry/logging captures lifecycle with correlation IDs and error taxonomy.
