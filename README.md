# SadafApplication  
### Multi-Tenant Visa Processing Platform – Backend Architecture & Engineering Report

This repository documents the complete backend design, development workflow, and architecture of **SadafApplication**, a production-ready **multi-tenant Visa Processing Platform** engineered using **FastAPI, PostgreSQL, SQLAlchemy, AWS S3, and JWT authentication**.

The project is built to support **real visa agencies**, enabling them to manage customers, files, visa requests, accounting operations, and hierarchical access — all inside a clean, scalable backend infrastructure.

This report is intentionally detailed to highlight the engineering decisions, patterns, and systems I implemented, and is suitable for inclusion in a professional CV, portfolio, or technical interview.

---

## 🔹 Overview

SadafApplication is a **two-service architecture**:

### **1. CoreApp (Backend Engine)**
The central API service responsible for:
- Authentication (JWT-based)
- Agency hierarchy & permissions
- Visa processing workflows
- Document storage (AWS S3)
- Accounting transactions
- Audit logging
- Future integrations (Kafka, Redis, Lambda)

### **2. PanelApp (Dashboard Application)**
A FastAPI + Jinja2 application serving:
- Agency dashboards
- Visa request UI
- File upload flows
- Accounting pages
- User management
- Token-based communication with CoreApp

This separation enables a clean division of responsibilities and prepares the system for API-first scaling.

---

## 🔹 Core Features Implemented

### **1. Multi-Tenant Architecture**
The system supports:
- SuperAdmin (Sadaf)
- Agencies
- Sub-agencies
- Agents
- Customers  

Each agency has **full isolation** of:  
customers, visa requests, accounting records, file uploads, and logs.

Access control is fully rule-based and enforced in both CoreApp & PanelApp.

---

### **2. Authentication & Security**
I implemented:
- Centralized authentication in CoreApp  
- PanelApp ↔ CoreApp token exchange  
- JWT sessions 
- Device-based login restriction (one device at a time)  
- Manager-only password resets  
- Route-level role enforcement  
- Full audit logging for every sensitive action  

Security and traceability were core engineering priorities.

---

### **3. Visa Request Engine**
A rich visa workflow that includes:
- Customer data entry  
- Task-based document collection  
- AWS S3 upload integration  
- Metadata saved per file:  
  `file_name`, `upload_date`, `s3_path`  
- Status management (pending, completed, rejected)  
- Full audit trail per request  

All documents are stored **within the VisaRequest.tasks structure** for maximum clarity and traceability.

---

### **4. Accounting System (In Progress / Phase 2)**
A modular, agency-scoped accounting subsystem with:
- Transaction records (invoice, payment, refund)
- Linking to `agency_id`, `visa_request_id`, `customer_id`, `created_by`
- Support for payment methods (cash, card, bank transfer)
- Reporting per agency
- Future support for commissions, settlements, and automated invoicing

The accounting logic is designed to reflect real-world agency operations.

---

### **5. Logging & Audit Trail**
Every critical event is logged with:
- `user_id`, `agency_id`
- Action type
- Timestamp
- Metadata  
- IP & user context

This ensures a transparent, legally traceable system suitable for real visa businesses.

---

### **6. File Management (AWS S3)**
Files uploaded inside PanelApp are:
- Validated  
- Stored in S3  
- Saved with metadata  
- Linked directly to a VisaRequest task  

No flat "files table" — everything is contextual and structured.

---

## 🔹 Technical Stack

### **Backend**
- FastAPI  
- SQLAlchemy ORM  
- Alembic (Migrations)  
- PostgreSQL  
- Pydantic v2  
- JWT Authentication  

### **Infrastructure**
- AWS S3 (document storage)  
- AWS EC2 (deployment)  
- Nginx (reverse proxy)  
- Docker-ready structure  

### **Future Integrations**
- Redis (sessions)  
- Kafka (event logging)  
- AWS Lambda (background tasks)  
- Prometheus/Grafana (monitoring)

---

## 🔹 Engineering Highlights (CV-Relevant)

This project demonstrates:

### **✔ Backend Architecture Design**
I designed a clean, modular, production-grade backend with separated services, consistent schema validation, and multi-tenant constraints.

### **✔ API-First Development**
CoreApp acts as a strict backend engine, enabling future:
- Mobile apps  
- Partner integrations  
- Third-party automation  

### **✔ Real-World Security Practices**
Including:
- JWT  
- Role-based permissions  
- Device policy  
- Manager-only resets  
- Full audit logging  

### **✔ Database & Schema Architecture**
Normalised PostgreSQL tables for:
- Agencies  
- Users  
- Visa requests  
- Tasks  
- Accounting transactions  
- Audit logs  

### **✔ Enterprise-Level Workflow Engineering**
Visa and Accounting modules were designed to match real business processes.


Clear separation of modules ensures maintainability and scalability.

---

## 🔹 What This Repository Is For

This repository serves as:
- A **technical portfolio piece** showcasing backend engineering depth  
- A **reference document** for collaborative work  
- A **CV-ready demonstration** of multi-tenant system design  
- A foundation for launching a real B2B visa service  

---

## 🔹 Author

**Amir Tabatabaei**  
ML/AI Engineer & Backend Developer  
LinkedIn: https://www.linkedin.com/in/amirtabatabaei10/  

---

## 🔹 License

This project is currently private and proprietary.  
Contact the author regarding access or collaboration.
~~~

