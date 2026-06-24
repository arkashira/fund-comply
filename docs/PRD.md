# Product Requirements Document (PRD)  
**Project:** fund‑comply  
**Owner:** Axentx Product Team  
**Last Updated:** 2026‑06‑24  

---

## 1. Problem Statement  

Small and medium‑sized investment funds (AUM $10M‑$500M) face a growing regulatory burden:  

| Regulation | Typical Compliance Activity | Pain Point |
|------------|----------------------------|------------|
| **SEC Form N‑Q/N‑P** | Quarterly NAV & performance reporting | Manual aggregation, spreadsheet errors |
| **FINRA 24‑8** | Trade confirmation & settlement reconciliation | Time‑consuming reconciliation, high audit risk |
| **MiFID II** | Client order and transaction reporting | Complex data mapping, frequent rule changes |
| **AML/KYC** | Ongoing client due‑diligence | Continuous monitoring, data silos |

These funds lack dedicated compliance teams and often rely on manual processes or expensive legacy software. The result is:

- **High operational cost** (staff time, external consultants).  
- **Increased risk** of regulatory fines due to errors or late filings.  
- **Lost competitive advantage** as larger funds can automate faster.

---

## 2. Target Users  

| Persona | Role | Key Pain Points | Desired Outcomes |
|---------|------|-----------------|------------------|
| **Compliance Officer** | Head of Compliance | Overseeing multiple funds, ensuring accuracy | One‑stop dashboard, automated alerts |
| **Operations Lead** | Operations Manager | Manual data pulls, reconciliation | Time savings, fewer manual steps |
| **Fund Manager** | Portfolio Manager | Quick access to regulatory reports | Transparent reporting, reduced admin |
| **CFO/Finance** | Finance Director | Cost control, audit readiness | Cost‑effective solution, audit trail |

*All personas operate within funds that have 5‑50 staff and limited IT budgets.*

---

## 3. Goals & Success Metrics  

| Goal | Success Metric | Target |
|------|----------------|--------|
| **Reduce compliance cycle time** | Avg. days from data capture to filing | < 5 days |
| **Increase accuracy** | Error rate in filed reports | < 0.5 % |
| **Lower operating cost** | % of compliance budget spent on manual labor | < 20 % |
| **Improve user satisfaction** | NPS score | ≥ 70 |
| **Regulatory coverage** | % of required reports auto‑generated | 100 % (initial scope) |

---

## 4. Key Features (Prioritized)  

| # | Feature | Description | Priority | Dependencies |
|---|---------|-------------|----------|--------------|
| 1 | **Data Ingestion & Normalization** | Connect to fund data sources (CRM, trading platform, custodians) via APIs or CSV uploads; map to internal schema. | Must‑Have | API connectors, data model |
| 2 | **Regulation Engine** | Rule‑based engine that translates regulatory requirements into data transformations and validation checks. | Must‑Have | Data model, rule repository |
| 3 | **Automated Report Generation** | Generate PDF/Excel/XLSX reports per regulation (N‑Q, 24‑8, MiFID II, AML). | Must‑Have | Regulation Engine, templates |
| 4 | **Audit Trail & Versioning** | Immutable log of data changes, report versions, and user actions. | Must‑Have | Database, logging |
| 5 | **Dashboard & Alerts** | Real‑time status of compliance tasks, overdue items, error notifications. | Must‑Have | Front‑end UI, notification service |
| 6 | **Self‑Service Rule Updates** | Non‑technical users can add/modify compliance rules via a guided UI. | Should‑Have | Rule editor, validation |
| 7 | **Multi‑Fund Management** | Manage multiple funds under a single tenant with isolation. | Should‑Have | Multi‑tenant architecture |
| 8 | **Export & Integration** | API endpoints for downstream systems (e.g., accounting, audit). | Nice‑to‑Have | API layer |
| 9 | **Compliance Calendar** | Calendar view of upcoming filing deadlines. | Nice‑to‑Have | Calendar UI |
|10 | **AI‑Assisted Data Mapping** | Use LLM to suggest field mappings and flag anomalies. | Nice‑to‑Have | vLLM integration |

---

## 5. Scope (In‑Scope)

- Core compliance reporting for SEC N‑Q/N‑P, FINRA 24‑8, MiFID II, AML/KYC.
- Data ingestion from CSV, Excel, and REST APIs (initially 3 key custodians).
- Web‑based UI (React) + backend (FastAPI + PostgreSQL).
- Single‑tenant deployment (initial release).
- Automated PDF/Excel report generation with pre‑defined templates.
- Audit trail and versioning for all data and reports.
- Basic dashboard with status tiles and email alerts.

## 6. Scope (Out‑of‑Scope)

- Full‑scale enterprise multi‑tenant SaaS (will be added in v2.0).
- Integration with all possible custodians; only 3 will be supported initially.
- Advanced AI‑driven anomaly detection (planned for future releases).
- Mobile app (web responsive only for now).
- Custom regulatory rule creation by non‑technical users (rule editor will be basic).

---

## 7. Technical Constraints & Assumptions  

| Constraint | Impact | Mitigation |
|------------|--------|------------|
| **Regulatory change velocity** | Frequent updates to rules | Modular rule engine, versioned rule sets |
| **Data privacy** | Sensitive client data | Encrypted storage, role‑based access |
| **Performance** | Large data volumes (up to 1M rows per fund) | Batch processing, async workers |
| **Compliance of the tool itself** | Must meet SOC2/ISO 27001 | Adopt existing Axentx security framework |

---

## 8. Milestones  

| Milestone | Deliverable | Target Date |
|-----------|-------------|-------------|
| **MVP 1.0** | Core ingestion, rule engine, report generation, audit trail | 2026‑08‑15 |
| **Beta Release** | Dashboard, alerts, basic multi‑fund | 2026‑10‑01 |
| **Public Launch** | Full feature set, documentation, onboarding | 2026‑12‑01 |

---

## 9. Success Criteria  

1. **User Adoption** – ≥ 30 active users within 3 months post‑launch.  
2. **Compliance Accuracy** – 0 major errors in first 6 compliance cycles.  
3. **Operational Savings** – 40 % reduction in manual hours reported by beta users.  
4. **Regulatory Coverage** – All required reports auto‑generated without manual intervention.  

---

## 10. Risks & Mitigations  

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| **Regulatory changes** | Medium | High | Modular rule engine, continuous monitoring |
| **Data source incompatibility** | Medium | Medium | Flexible ingestion layer, fallback CSV |
| **User resistance to automation** | Low | Medium | Training, user‑friendly UI, phased rollout |
| **Security breach** | Low | High | SOC2 controls, encryption, audit logs |

---

## 11. Dependencies  

- **Axentx Knowledge Base** – for regulatory rule definitions.  
- **vLLM** – optional AI assistance for data mapping.  
- **SGLang** – structured generation for report templates.  
- **Existing Axentx infrastructure** – authentication, logging, monitoring.

---

## 12. Acceptance Criteria  

1. **Data ingestion** validates against schema and flags errors.  
2. **Rule engine** correctly applies all regulatory rules and produces compliant outputs.  
3. **Reports** match regulatory templates and pass sample validation tests.  
4. **Audit trail** records every data change and report generation event.  
5. **Dashboard** displays real‑time status and sends alerts for overdue items.  
6. **Performance**: 95% of reports generated in < 2 minutes for 100k rows.  

---

## 13. Glossary  

- **N‑Q/N‑P** – SEC quarterly NAV and performance reports.  
- **24‑8** – FINRA trade confirmation and settlement reconciliation.  
- **MiFID II** – EU regulatory framework for investment services.  
- **AML/KYC** – Anti‑Money Laundering / Know‑Your‑Customer compliance.  

---

*Prepared by: Senior Product Lead, Axentx*
