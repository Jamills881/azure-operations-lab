# Architecture

## Current Status

* **Phase 1 — Foundation:** Completed
* **Phase 2 — Security & Identity:** In Progress (mostly completed)
* **Phase 3 — Monitoring & Operations:** Planned
* **Phase 4 — Automation:** Planned
* **Phase 5 — Advanced Networking & Security:** Planned

---

# Phase 1 — Foundation

The initial Azure environment contains the foundational resources needed to support future networking, monitoring, security, and automation.

---

### Resource Group

**Status:** Completed

**Purpose:** Provide a logical container for all project resources.

---

### Storage Account

**Status:** Completed

**Purpose:** Store project files and provide exposure to Azure Storage concepts such as blobs, access control, monitoring, and logging.

---

### Log Analytics Workspace

**Status:** Completed

**Purpose:** Serve as the central location for monitoring data, diagnostics, and future alerting.

---

### Virtual Network

**Status:** Completed

**Purpose:** Provide private networking for Azure resources and introduce core infrastructure concepts such as address spaces and subnets.

---

### Network Security Group

**Status:** Completed

**Purpose:** Control inbound and outbound network traffic using firewall-style security rules applied to `subnet-main`.

---

### App Service

**Status:** Paused

**Purpose:** Originally intended to host a simple web application that could later be monitored, secured, and automated.

**Current Issue:** Deployment is blocked by a `Microsoft.Web/serverFarms` subscription/quota-related validation error.

**Decision:** App Service is paused and does not currently block project progress.

---

### Virtual Machine

**Status:** Completed

**Purpose:** Provide a compute workload inside the virtual network so networking, security, and monitoring can be tested using a real resource.

---

# Phase 2 — Security & Identity

This phase focuses on securing application secrets, identity-based authentication, and access control between Azure resources.

---

### Key Vault

**Status:** Completed

**Purpose:** Securely store secrets, passwords, certificates, and other sensitive configuration data.

---

### Managed Identity

**Status:** Completed

**Purpose:** Provide Azure resources with an identity in Microsoft Entra ID so they can authenticate to Azure services without storing credentials locally.

---

### Azure SQL Database

***Status:*** Completed

***Purpose:*** Provide a managed relational database service that integrates with identity, security, and application workloads while introducing Azure PaaS database administration concepts.
---

### Security Relationships

Current identity and secret access flow:

Virtual Machine
↓
System Assigned Managed Identity
↓
RBAC Role Assignment
↓
Azure Key Vault
↓
Secret Access

---

# Phase 3 — Monitoring & Operations

Planned focus areas:

* Azure Monitor
* Diagnostic Settings
* Alerts

---

# Phase 4 — Automation

Planned focus areas:

* PowerShell Automation
* Bicep Deployments

---

# Phase 5 — Advanced Networking & Security

Planned focus areas:

* Additional subnets
* Security hardening
* Documentation refinement
