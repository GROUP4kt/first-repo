# Ubuntu Enterprise Hub (UEH) — Day 4 Sprint Backlog & Task Allocation

## 📌 Executive Summary & Sprint Goal
This document defines the official **Sprint Backlog** and **Task Allocation Matrix** for the **Ubuntu Enterprise Hub (UEH)** development team. Developed as part of the **Day 4 Design Stage Sign-off**, this backlog breaks down the requirements (`FR-1.1` to `FR-4.1`), security controls (`SEC-1.1` to `SEC-1.5`), database tables (`users`, `service_requests`, `ticket_logs`, `opportunities`, `opportunity_applications`), and wireframe designs into concrete, actionable development tasks for **Days 5 through 15**.

---

## 👥 Team Operational Rules & Habits
* **Daily Stand-up:** 10-minute daily morning alignment (Yesterday's progress, Today's goals, Blockers).
* **Mandatory Daily Commit:** Regardless of current role, **every team member must write code and submit at least one Git commit daily** with clean, conventional commit messages.
* **Role Rotation Schedule:** Formally log role changes on **Day 5**, **Day 9**, and **Day 13**.
* **Branch Strategy:** Work on isolated feature branches (`feature/`, `docs/`), integrate via pull requests into `dev`, and deploy stable releases to `main`.

---

## 📋 Comprehensive Backlog Breakdown

### **Module 1: Infrastructure, Project Setup & Security (Day 5)**
| Task ID | Task Description | Target Requirement | Deliverable |
| :--- | :--- | :--- | :--- |
| **TASK-01** | Initialize Django REST Framework backend project inside `backend/` directory. | Core Setup | Django project structure & `settings.py` |
| **TASK-02** | Initialize React frontend application using Vite/CRA inside `frontend/` directory. | Core Setup | React app shell & routing setup |
| **TASK-03** | Configure `.env` environment variables and updated `.gitignore` for secret keys. | `SEC-1.5` | Operational `.env.example` & safe repo |
| **TASK-04** | Configure SQLite/PostgreSQL database connections in backend settings. | Core Setup | Verified DB connection setup |

---

### **Module 2: Database Models & Migrations (Day 5 – Day 6)**
| Task ID | Task Description | Target Requirement | Deliverable |
| :--- | :--- | :--- | :--- |
| **TASK-05** | Implement `User` model with custom user manager, password hashing, and role choices (`MSME_CLIENT`, `SUPPORT_AGENT`, `ADMIN`). | `FR-1.2`, `SEC-1.1` | `User` class in `models.py` |
| **TASK-06** | Implement `ServiceRequest` and `TicketLog` models with foreign key links to `User`. | `FR-2.1`, `FR-2.3` | `ServiceRequest` & `TicketLog` models |
| **TASK-07** | Implement `Opportunity` and `OpportunityApplication` models with `UNIQUE(opportunity_id, client_id)`. | `FR-3.1`, `FR-3.4` | `Opportunity` & `Application` models |
| **TASK-08** | Execute initial Django migrations (`makemigrations` / `migrate`) and seed initial admin superuser. | System DB | Clean schema in database |

---

### **Module 3: Authentication & Role-Based Access Control APIs (Day 6 – Day 7)**
| Task ID | Task Description | Target Requirement | Deliverable |
| :--- | :--- | :--- | :--- |
| **TASK-09** | Build `POST /api/auth/register/` and `POST /api/auth/login/` endpoints. | `US-01`, `US-02` | Token/Session Auth APIs |
| **TASK-10** | Implement server-side DRF permission classes for RBAC (`IsMSMEClient`, `IsSupportAgent`, `IsAdmin`). | `SEC-1.4` | `permissions.py` module |
| **TASK-11** | Add backend payload validation and CSRF middleware integration. | `SEC-1.2`, `SEC-1.3` | Input validation rules |

---

### **Module 4: Helpdesk & Support Request Engine (Day 7 – Day 8)**
| Task ID | Task Description | Target Requirement | Deliverable |
| :--- | :--- | :--- | :--- |
| **TASK-12** | Build `POST /api/tickets/` and `GET /api/tickets/` endpoints. | `FR-2.1`, `FR-2.4` | Ticket CRUD API endpoints |
| **TASK-13** | Build `PATCH /api/tickets/{id}/status/` endpoint to record state transitions in `TicketLog`. | `FR-2.3` | Status update API & logger |
| **TASK-14** | Build React Support Ticket Logging Form & Client Tracking Dashboard UI. | `US-04`, `US-05` | `ClientHelpdeskView.jsx` |
| **TASK-15** | Build React Support Agent Queue & Ticket Status Update Panel UI. | `US-06` | `AgentQueueView.jsx` |

---

### **Module 5: Growth Opportunities & Admin Analytics (Day 9 – Day 11)**
| Task ID | Task Description | Target Requirement | Deliverable |
| :--- | :--- | :--- | :--- |
| **TASK-16** | Build `GET /api/opportunities/` and `POST /api/opportunities/` endpoints. | `FR-3.1`, `FR-3.3` | Opportunity API endpoints |
| **TASK-17** | Build `POST /api/opportunities/{id}/apply/` preventing duplicate submissions. | `FR-3.4` | Application API endpoint |
| **TASK-18** | Build `GET /api/admin/dashboard/` real-time metrics aggregation endpoint. | `FR-4.1` | Admin Dashboard API |
| **TASK-19** | Build React Admin Analytics Dashboard & Opportunity Management View UI. | `US-07`, `US-11` | `AdminDashboardView.jsx` |
| **TASK-20** | Build React Public Homepage & Service Directory Category Grid UI. | Wireframe Mockup | `HomePage.jsx` |

---

## 🎯 Task Allocation Matrix (Initial Sprint Alignment)

Every team member is assigned lead ownership for specific backlog tasks while maintaining daily coding requirements:

| Role Title | Primary Responsibilities | Allocated Backlog Tasks |
| :--- | :--- | :--- |
| **Team Lead** | Repository Architecture, Security Setup & Auth APIs | `TASK-01`, `TASK-03`, `TASK-04`, `TASK-09`, `TASK-10` |
| **Systems Analyst** | Database Integrity, Model Layer & API Contracts | `TASK-05`, `TASK-06`, `TASK-07`, `TASK-08`, `TASK-17` |
| **Developer 1 (Backend/Full-Stack)** | Service Ticket Engine & Audit Logging APIs | `TASK-11`, `TASK-12`, `TASK-13`, `TASK-16`, `TASK-18` |
| **Developer 2 (Frontend Lead)** | React Router, UI Views & Responsive Dashboards | `TASK-02`, `TASK-14`, `TASK-15`, `TASK-19`, `TASK-20` |
| **Tester / Quality Lead** | Security Validation, Integration Testing & API Defense | `TASK-10`, `TASK-11`, Test Suites & Security Verification |

---

## 🌿 Git Branching Strategy & Workflow Rules

```text
main (Production Releases)
 │
 └── dev (Integration Branch)
      ├── feature/auth-api          <-- Team Lead
      ├── feature/database-models   <-- Analyst
      ├── feature/helpdesk-api      <-- Developer 1
      ├── feature/react-dashboards  <-- Developer 2
      └── docs/sprint-backlog       <-- Quality Lead / All
```

1. **Checkout Feature Branch:** `git checkout -b feature/<task-name>`
2. **Commit Changes Daily:** `git commit -m "feat(auth): implement login endpoint validation"`
3. **Push & Open PR:** Push branch to remote and submit Pull Request into `dev`.
4. **Merge to Dev:** Require at least one peer review sign-off before merging into `dev`.

---

## ✅ Day 4 Sign-Off & Day 5 Readiness Checklist
- [x] All 5 ERD tables fully mapped to backlog tasks (`TASK-05` to `TASK-08`).
- [x] All REST API specifications mapped to backend endpoints (`TASK-09` to `TASK-18`).
- [x] All 4 UI wireframe views mapped to React components (`TASK-14` to `TASK-20`).
- [x] Security requirements (`SEC-1.1` to `SEC-1.5`) integrated into initial backend tasks.
- [x] Tasks allocated to all team members with daily commit requirements.
