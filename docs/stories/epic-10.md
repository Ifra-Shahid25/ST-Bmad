# EPIC 10 - Reports & Dashboards

### Story 10.1 Reporting and Queueing
User Story: As a reporting user, I want parameterized reports with queueing so that long jobs do not block UI.
Acceptance:
- C1 FlexReports accept parameters and queue long jobs with status/progress.
- Exports (PDF/Excel/CSV) respect masking/permissions; prevent duplicate/overlapping runs.
- Telemetry/error taxonomy logged; UI remains responsive.

### Story 10.2 Dashboards
User Story: As a manager, I want dashboards of key KPIs so that I can monitor operations quickly.
Acceptance:
- KPIs include exceptions/aging, scheduler health, licensing, report/import/OCR queues.
- Refresh configurable; views role-scoped; exports audited and masked.
- Performance avoids UI blocking; alert thresholds definable.
