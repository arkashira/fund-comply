# STORIES.md

## Project: **fund‑comply**

Automated compliance and reporting tool for small and medium‑sized investment funds.  
The goal is to reduce manual effort, eliminate errors, and ensure timely submission of regulatory reports.

---

## Epics & Story Backlog

| Epic | Story | Acceptance Criteria |
|------|-------|---------------------|
| **Data Ingestion** | **S1** | **As a** compliance analyst, **I want** to upload fund data in CSV/Excel, **so that** the system can ingest and validate it automatically. | • Supports CSV, XLSX, and JSON.<br>• Validates required columns (e.g., `AssetID`, `NAV`, `Date`).<br>• Returns clear error messages for missing/invalid fields.<br>• Stores raw file in secure S3 bucket. |
| | **S2** | **As a** data engineer, **I want** the system to automatically pull data from the fund’s internal API, **so that** I don’t need to upload files manually. | • Supports OAuth2 authentication.<br>• Pulls data every 30 min via scheduled job.<br>• Logs success/failure and retries on transient errors.<br>• Stores data in the same schema as S1. |
| | **S3** | **As a** compliance analyst, **I want** to map incoming data fields to internal schema, **so that** the system can standardize data for downstream processing. | • UI wizard for field mapping.<br>• Saves mapping profiles.<br>• Allows re‑use of profiles for future uploads.<br>• Validates mapping against required schema. |
| **Compliance Rules Engine** | **S4** | **As a** compliance officer, **I want** the system to run a set of predefined regulatory rules on the ingested data, **so that** I can quickly identify violations. | • Implements at least 10 core rules (e.g., NAV threshold, concentration limits).<br>• Rules are configurable via JSON.<br>• Produces a rule‑violation report with actionable insights.<br>• Supports rule versioning. |
| | **S5** | **As a** compliance officer, **I want** to create custom rules using a simple DSL, **so that** I can adapt to new regulations. | • DSL supports `IF`, `THEN`, `ELSE` constructs.<br>• DSL is parsed into an internal rule engine.<br>• Provides syntax highlighting and linting in the UI.<br>• Unit tests for DSL parser. |
| | **S6** | **As a** compliance officer, **I want** the system to flag data that fails any rule, **so that** I can investigate before reporting. | • Violations are highlighted in the UI.<br>• Violations can be annotated and saved.<br>• Audit trail of all rule evaluations. |
| **Reporting & Export** | **S7** | **As a** compliance analyst, **I want** to generate regulatory reports in PDF and XML formats, **so that** I can submit them to regulators. | • PDF and XML templates are configurable.<br>• Reports include metadata (report ID, date, fund ID).<br>• Supports batch generation.<br>• Exported files are signed with a digital certificate. |
| | **S8** | **As a** compliance analyst, **I want** to schedule report generation, **so that** I don’t have to run it manually each month. | • UI for scheduling (cron syntax).<br>• Sends email notification on completion.<br>• Stores schedule in database. |
| | **S9** | **As a** compliance analyst, **I want** to preview a report before export, **so that** I can catch formatting issues early. | • Live preview pane in UI.<br>• Supports pagination and zoom.<br>• Allows editing of placeholder data. |
| **Audit & Security** | **S10** | **As a** security officer, **I want** all data access to be logged, **so that** we can audit compliance. | • Audit log includes user, action, timestamp, IP.<br>• Logs are immutable and stored in a separate S3 bucket.<br>• Exports audit logs in CSV. |
| | **S11** | **As a** compliance officer, **I want** role‑based access control, **so that** only authorized users can view sensitive data. | • RBAC with roles: Admin, Analyst, Viewer.<br>• UI hides/locks features based on role.<br>• Role changes trigger audit log. |
| | **S12** | **As a** compliance officer, **I want** the system to encrypt data at rest and in transit, **so that** we meet regulatory security standards. | • Uses AES‑256 for data at rest.<br>• TLS 1.3 for all network traffic.<br>• Key management via AWS KMS. |
| **Integration & Extensibility** | **S13** | **As a** integration engineer, **I want** an API to fetch processed data, **so that** other systems can consume it. | • RESTful API with pagination.<br>• Supports OAuth2 and API keys.<br>• Returns JSON with HATEOAS links. |
| | **S14** | **As a** integration engineer, **I want** webhooks for rule violations, **so that** downstream systems can react automatically. | • Configurable webhook URLs.<br>• Payload includes violation details.<br>• Supports retry logic. |
| | **S15** | **As a** product manager, **I want** a plugin architecture, **so that** we can add new regulatory modules without redeploying. | • Plugins are Python packages loaded at runtime.<br>• Plugin API documented and versioned.<br>• Hot‑reload support for dev. |

---

## MVP Order (Sprint Planning)

1. **Sprint 1** – S1, S2, S3 (Data Ingestion)
2. **Sprint 2** – S4, S5, S6 (Compliance Rules Engine)
3. **Sprint 3** – S7, S8, S9 (Reporting & Export)
4. **Sprint 4** – S10, S11, S12 (Audit & Security)
5. **Sprint 5** – S13, S14, S15 (Integration & Extensibility)

---

## Definition of Done (DoD)

- Unit tests ≥ 90 % coverage for each module.  
- Integration tests for end‑to‑end flows.  
- Code reviewed and merged via PR.  
- Documentation updated (README, API docs, user guide).  
- Deployment to staging environment with smoke tests.  
- Acceptance criteria fully satisfied and signed off by product owner.  

---
