# TECH_SPEC.md

> **Project:** Data Shield  
> **Repository:** `axentx/data-shield`  
> **Owner:** Axentx Autonomous AI‑Workforce  
> **Last Updated:** 2026‑06‑12  

---

## 1. Executive Summary

Data Shield is a **proactive data‑protection platform** that gives power users full visibility and control over data deletions and modifications. It continuously monitors data stores, emits pre‑emptive notifications, and exposes a transparent audit portal and a user control panel. The system is built to satisfy regulatory compliance (GDPR, CCPA, etc.) while remaining lightweight, cloud‑native, and easily extensible.

---

## 2. Architecture Overview

```
┌───────────────────────┐
│  Client (Web UI)      │
│  (React + Vite)       │
└────────────┬───────────┘
             │
             ▼
┌───────────────────────┐
│  API Gateway (FastAPI) │
│  (REST + WebSocket)    │
└───────┬───────┬───────┘
        │       │
        ▼       ▼
┌───────────────┐  ┌───────────────────────┐
│  Notification │  │  Transparency Service  │
│  Service (Celery)│  │  (Audit & History API) │
└───────┬───────┘  └───────┬─────────────────┘
        │                 │
        ▼                 ▼
┌───────────────────────┐  ┌───────────────────────┐
│  Data Monitor (Debezium)│  │  User Control Service │
│  (Kafka → CDC)          │  │  (Preserve / Reject)  │
└───────┬───────┬───────┘  └───────┬─────────────────┘
        │       │                 │
        ▼       ▼                 ▼
┌───────────────────────┐  ┌───────────────────────┐
│  PostgreSQL (RDS)      │  │  Redis (Cache / Pub/Sub) │
└───────────────────────┘  └───────────────────────┘
```

* **Client** – Single‑page React app that consumes REST and WebSocket endpoints.
* **API Gateway** – FastAPI application exposing CRUD, notification, and audit endpoints.
* **Data Monitor** – Debezium + Kafka capture change events from PostgreSQL.
* **Notification Service** – Celery workers that send email/SMS/webhook alerts.
* **Transparency Service** – Provides immutable audit logs and a portal for users to review changes.
* **User Control Service** – Exposes endpoints for users to preserve or reject pending changes.
* **Data Store** – PostgreSQL for relational data; Redis for caching and pub/sub.
* **Observability** – OpenTelemetry traces, Prometheus metrics, Grafana dashboards.

---

## 3. Core Components & Interfaces

| Component | Responsibility | Key Interfaces |
|-----------|----------------|----------------|
| **Business Layer** (`business/`) | Domain models, use‑case services, validation | `DataMonitor`, `NotificationService`, `AuditService`, `UserControlService` |
| **API Layer** (`api/`) | REST/WebSocket endpoints, request/response schemas | `DataController`, `NotificationController`, `AuditController`, `ControlController` |
| **Worker Layer** (`workers/`) | Background jobs (email, SMS, webhook) | `NotificationWorker`, `AuditWorker` |
| **Infrastructure Layer** (`infra/`) | Docker, Helm, Terraform, CI/CD | `Dockerfile`, `helm/`, `terraform/` |
| **UI Layer** (`ui/`) | React SPA, authentication, dashboards | `DataTable`, `NotificationPanel`, `AuditView`, `ControlPanel` |

### 3.1 Business Interfaces

```python
class DataMonitor(Protocol):
    def watch_changes(self) -> Iterator[ChangeEvent]: ...

class NotificationService(Protocol):
    def notify(self, event: ChangeEvent, user: User) -> None: ...

class AuditService(Protocol):
    def record(self, event
