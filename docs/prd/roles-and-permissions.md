# Roles and Permissions 
- Roles: Loan Officer, Documentation Specialist, Compliance/Risk, Reporting/Board User, IT/Ops, Admin. 
- Modules/actions: view/create/edit/delete per entity; waivers (create/view) restricted to Documentation/Compliance/Admin; scheduler controls (start/stop/retry/view backlog) for IT/Ops/Admin; imports (dry-run/live) for IT/Ops/Admin; OCR approvals for Documentation/Compliance; exports for Reporting/Compliance/Admin with masking; config/preflight for IT/Ops/Admin. 
- Principle: least privilege; permission checks enforced in UI and services; unauthorized modules hidden or blocked with audit entry. 

### Role Profiles 
- Loan Officer: owns customer/loan creation and updates; can add notes/follow-ups; cannot waive docs; limited exports. 
- Documentation Specialist: manages documentation assignments/aging/waivers; uploads evidence; initiates notifications; cannot change config. 
- Compliance/Risk: approves waivers, reviews audit trails, accesses masked exports, oversees bureau/ComplianceOne pulls. 
- Reporting/Board User: runs reports/board reports, views dashboards, limited to export permissions set by Compliance/Admin. 
- IT/Ops: manages configs, schedulers, imports, service health, and preflight/diagnostics; can run test modes (NotificationTester/BRTestGen). 
- Admin: full permissions including roles/permissions management, config changes, and emergency overrides with audit. 
