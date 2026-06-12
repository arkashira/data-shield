# 📄 Data Shield – Product Requirements Document (PRD)

**Repository:** `github.com/axentx/data-shield`  
**Author:** Senior Product/Engineering Lead  
**Date:** 2026‑06‑12  

---  

## 1. Vision & Summary  
Data Shield empowers power‑users, data‑engineers, and compliance officers with **proactive visibility and control** over any data that is about to be **deleted or modified** in their systems. By delivering **timely notifications**, a **transparent audit portal**, and an **interactive control panel**, the product reduces accidental data loss, satisfies regulatory obligations (GDPR, CCPA, HIPAA, etc.), and builds trust with end‑users.

---

## 2. Problem Statement  

| Pain Point | Who Experiences It | Impact |
|------------|-------------------|--------|
| Unexpected data deletions or silent schema migrations cause production outages and loss of critical business intelligence. | Data engineers, SaaS product managers, compliance teams | Downtime, costly incident response, regulatory fines. |
| Auditors cannot easily prove *when* and *why* data was changed, leading to compliance gaps. | Compliance officers, legal teams | Failed audits, penalties, loss of customer confidence. |
| Users have no way to intervene before a destructive operation, forcing them to rebuild data from backups. | Power‑users, analysts | Time‑consuming restores, reduced productivity. |

**Result:** Organizations need a **single, low‑friction layer** that watches data stores, alerts stakeholders **before** destructive actions, and records a tamper‑proof log of what was changed and why.

---

## 3. Target Users & Personas  

| Persona | Primary Goals | Key Metrics |
|---------|---------------|-------------|
| **Data Engineer (Alex)** | Prevent accidental deletions during ETL jobs; maintain clean pipelines. | Reduction in post‑deployment rollbacks. |
| **Compliance Officer (Rita)** | Demonstrate audit‑ready logs for GDPR/CCPA. | % of audit queries answered automatically. |
| **Power‑User / Analyst (Sam)** | Preserve important datasets before they are purged. | Number of “preserve” actions taken per month. |
| **Product Manager (Leila)** | Ensure feature releases that modify data are transparent to customers. | NPS for data‑change transparency. |

---

## 4. Goals & Success Metrics  

| Goal | Success Metric | Target (12 mo) |
|------|----------------|----------------|
| **Proactive Protection** – users receive a heads‑up before any destructive data operation. | Avg. notification lead‑time (time between alert & operation) | ≥ 48 h |
| **Transparency & Audibility** – full, searchable log of every delete/modify event. | % of events with complete audit record | 100 % |
| **User Control** – users can “preserve”, “delay”, or “approve” pending operations. | % of pending operations acted on by users | ≥ 80 % |
| **Compliance Enablement** – support for GDPR “right to be forgotten” and similar mandates. | Number of compliance‑related tickets reduced | 70 % reduction |
| **Adoption** – product is used in at least 5 paying customers (or internal Axentx services). | Active paying customers | 5 |
| **Reliability** – system uptime & low false‑positive rate. | 99.9 % uptime, < 2 % false‑positive alerts | — |

---

## 5. Scope  

### 5.1 In‑Scope (MVP)  

1. **Data Monitoring Engine**  
   * Connectors for PostgreSQL, MySQL, MongoDB, and S3.  
   * Event capture for `DELETE`, `UPDATE`, `DROP`, and object lifecycle policies.  

2. **Notification System**  
   * Configurable channels: email, Slack webhook, and in‑app push.  
   * Lead‑time configuration (default 48 h).  

3. **Transparency Portal**  
   * Web UI (React + Tailwind) showing a chronological list of pending and completed events.  
   * Search & filter by table, user, timestamp, and reason.  

4. **User Control Panel**  
   * “Preserve”, “Delay”, “Approve”, “Reject” actions per event.  
   * Role‑based access control (RBAC) integrated with Axentx SSO.  

5. **Audit Log**  
   * Immutable append‑only log stored in PostgreSQL + signed JSON‑Web‑Token (JWT) entries for tamper evidence.  

6. **Basic Compliance Export**  
   * CSV/JSON export of audit logs for regulator submission.  

### 5.2 Out‑of‑Scope (Phase 2+)  

| Feature | Reason |
|---------|--------|
| **AI‑driven risk scoring** (e.g., using vLLM to predict impact) | Requires model training & dataset curation – slated for Phase 2. |
| **Full‑stack data‑lineage visualization** | Complex graph generation beyond MVP. |
| **Support for on‑premise proprietary DBs (Oracle, DB2)** | Prioritize open‑source & cloud‑native stores first. |
| **Self‑service SaaS multi‑tenant billing** | Initial launch will be a licensed on‑prem/enterprise offering. |
| **Real‑time streaming integration (Kafka,
