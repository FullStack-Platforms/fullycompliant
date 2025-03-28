# Project ComplianceTracker: Architecture & Development Guide

## 1. Project Goal

To build a multi-tenant, self-hostable (initially via Docker Compose) compliance tracking application inspired by tools like Vanta and FutureFeed, with robust security primitives inspired by MinIO and Vault.

**MVP Focus:**

*   User authentication and basic role-based access control (Admin, Contributor, Viewer).
*   Multi-tenant architecture (organizations/tenants).
*   Ability for developers to load compliance frameworks (starting with NIST 800-171r3) via structured data (JSON).
*   Frontend UI for users to view adopted frameworks/requirements within their organization.
*   Ability for users to update the status of controls (Implemented, Planned, N/A, etc.) and add implementation details.
*   Ability for users to upload evidence files (PDFs, screenshots, etc.) linked to specific controls.
*   Dashboard view summarizing compliance posture for selected frameworks within the organization.
*   Simple Markdown export capability for System Security Plan (SSP) data based on tracked controls and ODP values.

**Non-MVP (Future Considerations):**

*   Advanced SSP generation (customizable templates, DOCX/PDF).
*   Integration with security tools (e.g., Prowler).
*   Automated evidence gathering (Cloud APIs, Scanners).
*   Notifications and task assignment workflows (email, in-app).
*   Support for mapping between frameworks.
*   More granular permissions.
*   User self-signup / organization creation (vs. invite-only).

## 2. High-Level Architecture

```mermaid
graph LR
    User[User Browser] --> FE[Frontend UI (React)];
    FE --> API[Backend API (Go)];

    subgraph "Core Infrastructure (Tenant-Scoped Interactions)"
        API --> DB[(PostgreSQL DB)];
        API --> ObjStore[Object Storage (MinIO)];
        API -- Retrieve Secrets --> Vault[Secrets Mgmt (Vault)];
        API --> DocGen[SSP Generation Logic];
    end

    style User fill:#fff,stroke:#333,stroke-width:2px
    style FE fill:#ccf,stroke:#333,stroke-width:2px
    style API fill:#cfc,stroke:#333,stroke-width:2px
    style DB fill:#fcc,stroke:#333,stroke-width:2px
    style ObjStore fill:#fcc,stroke:#333,stroke-width:2px
    style Vault fill:#fcc,stroke:#333,stroke-width:2px
    style DocGen fill:#ffc,stroke:#333,stroke-width:2px