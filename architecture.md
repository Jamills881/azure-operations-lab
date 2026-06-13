# Architecture

## Phase 1 — Foundation

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

**Purpose:** Control inbound and outbound network traffic using firewall-style security rules applied to subnet-main.

---

### App Service

**Status:** Paused

**Purpose:** Originally intended to host a simple web application that could later be monitored, secured, and automated.

**Current Issue:**
Deployment is blocked by a `Microsoft.Web/serverFarms` subscription/quota-related validation error.

**Decision:**
App Service is paused and does not currently block project progress.

---

## Phase 2 — Security & Identity

Planned resources:

* Azure SQL Database
* Key Vault
* Managed Identity

---

## Phase 3 — Monitoring & Operations

Planned resources:

* Azure Monitor
* Diagnostic Settings
* Alerts

---

## Phase 4 — Automation

Planned resources:

* PowerShell Automation
* Bicep Deployments

---

## Phase 5 — Advanced Networking & Security

Planned improvements:

* Additional subnets
* Security hardening
* Documentation refinement
