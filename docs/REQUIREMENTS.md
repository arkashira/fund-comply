# Requirements Document  
**Project:** fund‑comply  
**Version:** 1.0.0  
**Date:** 2026‑06‑24  

---  

## 1. Overview  

fund‑comply is an **automated compliance and reporting tool** aimed at small‑ and medium‑sized investment funds (SMIFs). It streamlines the collection, validation, transformation, and filing of regulatory data required by jurisdictions such as the U.S. SEC (Form PF), EU AIFMD, and UK FCA. The system reduces manual effort, minimizes errors, and provides an auditable trail for regulators and internal auditors.

---  

## 2. Scope  

| In‑Scope | Out‑Of‑Scope |
|----------|--------------|
| • Data ingestion from common fund‑management systems (CSV, JSON, API) | • Full‑blown portfolio‑management functionality |
| • Mapping of fund data to regulatory schemas (SEC Form PF, AIFMD, MiFID II) | • Legal advice or interpretation of regulations |
| • Generation of filing‑ready reports (PDF, XBRL, CSV) | • Integration with legacy on‑prem ERP systems not exposed via API |
| • Role‑based access control, audit log, and versioned compliance packages | • Real‑time market data feeds (outside of compliance‑related fields) |
| • Scheduler for periodic compliance runs (monthly/quarterly) | • Custom regulatory frameworks not covered in the initial release |
| • RESTful API for third‑party automation | • Desktop‑only UI (the product is web‑first) |

---  

## 3. Functional Requirements  

| ID | Description |
|----|-------------|
| **FR‑1** | **User Management** – The system shall support creation, modification, and deletion of user accounts with roles: **Administrator**, **Compliance Officer**, **Analyst**, and **Viewer**. |
| **FR‑2** | **Authentication & Authorization** – Users shall authenticate via OAuth 2.0 (supporting SSO providers: Google, Azure AD, Okta). Authorization shall be enforced per role on all UI and API endpoints. |
| **FR‑3** | **Data Ingestion** – The platform shall accept fund data via: <br>• CSV upload (configurable column mapping) <br>• JSON REST API (POST `/api/v1/fund-data`) <br>• Direct connector to popular fund‑admin SaaS (e.g., **iLEVEL**, **Addepar**) using OAuth token. |
| **FR‑4** | **Schema Validation** – Ingested data shall be validated against a configurable JSON‑Schema for each supported regulation. Validation errors must be reported with line/field context. |
| **FR‑5** | **Regulatory Mapping Engine** – The system shall transform validated fund data into the target regulatory schema (e.g., SEC Form PF XML, AIFMD XBRL). Mapping rules shall be version‑controlled and editable by Administrators via a UI. |
| **FR‑6** | **Report Generation** – Users shall be able to generate compliance reports in the following formats: <br>• PDF (human‑readable) <br>• XBRL (machine‑readable) <br>• CSV (raw export) <br>Reports must include a **generation timestamp**, **data version**, and **digital signature**. |
| **FR‑7** | **Scheduling & Automation** – Compliance Officers shall schedule recurring runs (e.g., “Quarterly AIFMD filing”) with configurable triggers: **cron**, **event‑driven** (new data upload), or **manual**. |
| **FR‑8** | **Audit Trail** – Every action (data upload, mapping edit, report generation, user login) shall be recorded with: user ID, timestamp, IP address, and a hash of the affected payload. Audit logs must be immutable for at least 7 years. |
| **FR‑9** | **Versioned Compliance Packages** – Each generated report shall be stored as a **Compliance Package** containing: source data snapshot, mapping version, generated files, and audit log. Packages are retrievable via UI and API. |
| **FR‑10** | **Notification Service** – The system shall send email (or Slack webhook) notifications on: <br>• Successful report generation <br>• Validation failures <br>• Upcoming filing deadlines (configurable per jurisdiction). |
| **FR‑11** | **Export & Integration API** – Provide a read‑only REST API (`/api/v1/compliance-packages/{id}`) to fetch generated reports and metadata for downstream systems. |
| **FR‑12** | **Multi‑Jurisdiction Support** – The initial release shall support: <br>• U.S. SEC Form PF (annual) <br>• EU AIFMD (quarterly) <br>• UK FCA (annual) <br>Additional jurisdictions can be added via plug‑in mapping modules. |
| **FR‑13** | **Help & Documentation** – Context‑sensitive help links and a searchable knowledge base shall be available within the UI. |
| **FR‑14** | **Data Retention & Deletion** – Administrators shall configure retention policies (default 5 years). Deletion requests must purge data from primary storage and audit logs while preserving immutable audit entries for compliance. |

---
