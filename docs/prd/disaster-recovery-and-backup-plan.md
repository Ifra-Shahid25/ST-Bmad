# Disaster Recovery and Backup Plan 
- DB backups for LMS DB and BR DB with defined RPO/RTO targets (confirm with ops); test restore procedures; encrypt backups where applicable. 
- Back up configuration: INI/app.config, `[LMS] BACKEND` MSI artifacts (x64/x86), and third-party license assets; document restore steps. 
- Rollback: retain prior MSI packages; rollback procedure tested; audit rollback actions. 
- Logs and telemetry: rotation/retention defined; ensure availability for incident review; mask sensitive data. 
- Services: restart runbooks for Notification and Board Report schedulers; verify post-restart health/heartbeats. 
