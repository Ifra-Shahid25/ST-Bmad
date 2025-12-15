# Technical Assumptions 
 
### Repository Structure: Monorepo 
Single repo containing the WinForms app, shared modules, and supporting services/utilities; keep the existing module layout (Util, Data, Error, Customers, Loans, Collateral, DT, Reports, Dashboards, FollowUp, Configure, Lookup, FA, BR/BRSchedule, Credit Bureau, OCR/AI, Portal, TCP). 
 
### Service Architecture 
Monolith WinForms client with supporting Windows services (Notification, Board Report Scheduler); background workers/queues for long-running jobs; remain on .NET Framework 4.8 with `packages.config`. 
 
### Testing Requirements 
Unit and integration coverage for critical modules; harnesses for schedulers/imports (e.g., NotificationTester, BRTestGen) and import validation; manual regression for UI-heavy flows; telemetry-driven checks for schedulers/licensing. 
 
### Additional Technical Assumptions and Requests 
- ABBYY + Azure Document Intelligence keys/paths available; temp directories secured and cleaned. 
- ComponentOne/Spread/TX Text Control/Controls/Graphics DLLs validated per architecture (x86/x64) with runtime license checks. 
- INI chain `ST.Main.INI` -> `Suntell.ini` with `[LMS] BACKEND` for MSI/INI/docs; MSI shares may be local or UNC; arch-specific MSI folders (`MSI\\x64`, `MSI\\x86`). 
- Dual DB connections (LMS DB, BR DB) with encryption preferred; service accounts have Event Log/share/SMTP rights. 
- TCP ports 5000-5100 reserved for mobile/portal; enforce auth, rate limits, and logging. 
- Secrets not stored in plaintext; offline/air-gapped environments supported via bundled licensing assets/MSI shares. 
- Background jobs non-blocking; retries/backoff with idempotency and consistent error taxonomy (IO/API/Parsing/Quota). 
- Logging/telemetry sinks available with rotation/retention; correlation IDs for cross-service tracing. 

### Email Delivery Constraints 
- SMTP/STARTTLS auth required; rate limits and quiet hours configurable; retries/backoff with bounded attempts. 
- Error taxonomy applied (IO/API/Config); surface failures in scheduler status with remediation steps. 
- Audit/log notification sends with correlation IDs; mask sensitive content; support test mode (NotificationTester). 
 
### Architecture Guidance Updates 
- Telemetry/logging sinks: Event Log plus optional file/forwarder; structured logs with correlation IDs `{env}:{service}:{jobId}`. 
- Error taxonomy: IO/API/Parsing/Quota/Config/SQL applied across schedulers/OCR/imports. 
- MSI rollback: on failed update, revert to prior MSI from `[LMS] BACKEND`, re-validate DLLs per arch, and log/audit rollback with user/timestamp. 
- Dependency validation process: preflight DLL/license checks per arch (ComponentOne/Spread/TX/Controls/Graphics/ABBYY/Azure DI); block critical misses with guidance. 
- Temp hygiene: enforce secured, writable temp directories; clean after OCR/AI and imports; log cleanup outcomes. 
 