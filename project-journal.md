# Project Journal

## June 10, 2026

Started the Azure Operations Lab project.

### Project Goal

Build a practical Azure environment focused on infrastructure, networking, identity, monitoring, and automation — the core skills needed for Azure Administrator, Systems Administrator, Infrastructure Engineer, and Cloud Operations roles.

### Current Status

Planning phase. Reviewing previous Azure labs and organizing the new project direction.

### Next Task

Create the initial project structure and outline the architecture for Phase 1.

## June 10, 2026

Created the initial Resource Group for the Azure Operations Lab.

Resource Group:
- rg-operationslab-dev

Reason:
The Resource Group will be used to organize all Phase 1 Azure resources for the project.

Next task:
Create the Storage Account using a low-cost configuration.

Created Storage Account:

- stoperationslab01

Configuration:
- Standard Performance
- LRS Redundancy

Learned:
- Storage Accounts contain services such as Blob Storage.
- Access Keys and Shared Access Signatures can be used to grant access.
- Storage Accounts include built-in monitoring capabilities.

Next Task:
Explore Blob Containers and begin planning App Service deployment.

Personal Notes

My understanding:
A Storage Account provides several types of storage services, including Blob Storage, Files, Tables, and Queues. It serves as a central location for storing application and operational data.

Attempted to deploy an App Service using the Free F1 tier.

Result:
Deployment validation failed during App Service Plan creation.

Error:
Microsoft.Web/serverFarms reported a quota-related validation error.

Decision:
Pause App Service deployment and continue defining the project architecture while investigating the subscription limitation.

## Session Summary

Completed:
- Created Azure Operations Lab repository
- Defined project goals and scope
- Created Resource Group
- Created Storage Account

Issue Encountered:
- App Service deployment failed due to a Microsoft.Web/serverFarms quota validation error.

Decision:
- Document the issue and continue the project without letting a single deployment problem derail progress.

Next Session:
- Investigate App Service deployment issue.
- Finalize Phase 1 architecture.
- Continue building the Azure Operations Lab.

- ### June 11, 2026

**Created:**
Log Analytics Workspace — `law-operationslab-dev` in `rg-operationslab-dev` (East US)

**Reason:**
Added a monitoring foundation for the Azure Operations Lab. This workspace will collect logs and metrics from Azure resources and support future alerting and diagnostics.

**Next Task:**
Connect an Azure resource (Storage Account) to this workspace using diagnostic settings.

# Project Journal

---

## 2026-06-11 — Evening Session

Tonight I focused on validating the monitoring setup for the Storage Account and confirming that metrics were flowing into the Log Analytics Workspace.

Azure’s portal made this more confusing than expected, and I spent more time than planned trying to locate the correct diagnostic settings for blob service logs.

After reviewing the setup, I decided not to let this block project progress.

### Key Takeaways

* Storage Account metrics are successfully flowing into Log Analytics.
* Blob service logs are not currently configured.
* Blob logs are not required for the next project phases.

The important part is that the core monitoring foundation is working, and the Log Analytics Workspace is ready to support future monitoring scenarios such as VM insights, diagnostics, and alerting.

### Decision

Rather than getting stuck troubleshooting optional logging configuration, I chose to continue moving the project forward.

This reflects a practical operations mindset: not every issue needs to be solved immediately if it is not blocking progress.

### Current Status

Completed:

* Resource Group
* Storage Account
* Log Analytics Workspace
* Storage metrics integration

Current Issue:

* App Service remains paused due to subscription-related deployment issues.

### Next Step

Move into networking by creating the Virtual Network and continue building out the Azure Operations Lab foundation.

## 2026-06-12 — Virtual Network Session

Created Virtual Network:

* vnet-operationslab-dev

Configuration:

* Address Space: 10.0.0.0/16
* Subnet: subnet-main
* Subnet Range: 10.0.1.0/24

Reason:
Added foundational networking to the Azure Operations Lab.

Learned:

* A Virtual Network acts as a private network inside Azure.
* Subnets divide the VNet into smaller logical network segments.
* Azure resources such as VMs, private endpoints, and application services can be placed inside subnets.

Next Task:
Explore network security by adding a Network Security Group (NSG).

## 2026-06-12 — Network Security Group Session

Created Network Security Group:

* nsg-operationslab-main

Configuration:

* Region: East US
* Associated Resource Group: rg-operationslab-dev

Reason:
Added network security controls to the Azure Operations Lab to manage inbound and outbound traffic between Azure resources.

Learned:

* An NSG acts like a firewall for Azure networking.
* NSG rules determine which traffic is allowed or denied.
* Azure includes default inbound and outbound security rules.

Next Task:
Associate the NSG with a subnet and begin understanding how security rules affect traffic flow.

## 2026-06-12 — NSG Association Session

Associated Network Security Group with subnet:

* NSG: nsg-operationslab-main
* Virtual Network: vnet-operationslab-dev
* Subnet: subnet-main

Reason:
Applied security controls to the subnet so traffic can be filtered using NSG rules.

Learned:

* Creating an NSG alone does not protect resources.
* The NSG must be associated with a subnet or NIC.
* Once associated, all traffic entering or leaving resources in that subnet is evaluated against NSG rules.

Next Task:
Determine what workload should be deployed inside the subnet so networking and security can be tested further.

## 2026-06-13 — Virtual Machine Deployment Session

Created Linux Virtual Machine:

* vm-operationslab-linux01

Configuration:

* Region: East US (Zone 2)
* Size: Standard B1s
* Operating System: Ubuntu Server 24.04 LTS
* Authentication: SSH key
* Private IP: 10.0.0.4
* Public IP: Assigned by Azure

Reason:
Added a compute workload to the Azure Operations Lab so networking, security, and monitoring can be tested using a real resource.

Learned:

* A Virtual Machine is a software-based computer running in Azure.
* The VM was deployed inside the virtual network and protected by the subnet’s NSG.
* Even with a public IP, the VM is not automatically reachable from the internet.
* Inbound access depends on NSG rules.

Decision:
The Azure-created default subnet and public IP will remain for now since neither blocks project progress.

Next Task:
Connect the VM to Log Analytics and begin monitoring compute metrics and activity.

## 2026-06-13 — Cost Management Setup

Created Azure budget alerts for the lab subscription.

Configuration:

* Budget Limit: $10
* Forecast Alert: 80%
* Actual Cost Alert: 90%

Reason:
Added cost controls to prevent unexpected Azure charges while continuing to build the lab environment.

Learned:

* Azure budgets help monitor and control cloud spending.
* Forecast alerts provide proactive warnings based on projected usage.
* Cost alerts notify when actual spending reaches a defined threshold.

Next Task:
Continue building the lab while monitoring resource costs, especially VM compute usage.

## 2026-06-14 — VM Monitoring Investigation

### What Was Explored

Monitoring options for the Linux virtual machine were reviewed to better understand how Azure collects performance and diagnostic data.

The VM Insights dashboard showed Azure is already collecting basic platform metrics by default, including:

* CPU utilization
* Network traffic
* Disk I/O
* Availability status

These metrics were available without additional configuration.

Diagnostic settings and monitoring options were also reviewed to understand Azure’s different monitoring paths.

---

### Key Observations

Azure currently provides both legacy and modern approaches for VM monitoring.

* **Legacy monitoring** uses the Azure Diagnostics extension and sends guest diagnostics to a Storage Account.
* **Modern monitoring** uses Azure Monitor Agent (AMA), Data Collection Rules (DCRs), and workspace-based telemetry.

This highlighted an important distinction between:

* **Platform metrics** — metrics Azure collects automatically from the infrastructure layer
* **Guest OS metrics** — deeper operating system telemetry collected from inside the VM

Guest-level monitoring provides additional visibility into:

* Memory usage
* Running processes
* Filesystem utilization
* Operating system performance

---

### What Was Learned

* Basic platform metrics are available by default in Azure.
* Guest-level monitoring requires additional configuration.
* Azure is moving away from legacy diagnostics toward AMA and DCR-based monitoring.
* Enhanced monitoring introduces more configuration complexity and potential additional cost.

---

### Decision

Enhanced monitoring was not enabled at this stage.

**Reason:**
The enhanced monitoring path introduces additional complexity, including:

* Azure Monitor Agent configuration
* Data Collection Rules
* Additional telemetry configuration
* Potential extra cost

This does not block project progress and can be revisited later when deeper monitoring is needed.

---

### Real-World Connection

This monitoring workflow felt similar to infrastructure monitoring performed in VMware vSphere at Expedient, where alerts for high CPU usage, disk usage, and resource health were common.

The main difference is the monitoring stack.

Traditional environments relied on virtualization tools such as vSphere, while Azure uses cloud-native services such as Azure Monitor, Log Analytics, and Data Collection Rules.

---

### Why This Matters

Monitoring is a core responsibility in infrastructure and cloud administration.

Understanding the difference between default platform metrics and deeper guest telemetry is important for troubleshooting performance issues, resource health, and alerting strategy.

## 2026-06-16 — Key Vault Deployment

### What Was Built

Azure Key Vault was deployed as part of Phase 2 (Security & Identity).

Resource:

* kv-operationslab-jarrod

The vault was configured using the **RBAC permission model** to control access to secrets and other sensitive data.

---

### Key Observations

Secret creation initially failed with a **Forbidden** RBAC error.

This highlighted an important Azure security concept:

* **Control-plane access** — managing the Key Vault resource
* **Data-plane access** — accessing secrets, keys, and certificates

Permission to deploy and manage a Key Vault does not automatically grant permission to the secrets stored inside it.

Available permissions allowed:

* Key Vault deployment
* Resource management
* IAM configuration

Missing permissions prevented:

* Secret creation
* Secret retrieval

---

### What Was Learned

* Key Vault securely stores secrets, keys, and certificates.
* Azure separates resource management from secret access.
* RBAC can allow management access while still blocking data access.
* Least privilege is important when assigning access to sensitive resources.

---

### Challenges & Resolution

**Issue:** Secret creation blocked by RBAC
**Cause:** Missing data-plane permissions

**Resolution:**

* Reviewed IAM configuration
* Identified missing role assignment
* Assigned **Key Vault Secrets Officer** role
* Allowed time for RBAC propagation

**Outcome:** Secret creation succeeded and secret access became available.

---

### Real-World Connection

This closely resembles privileged credential vault systems used at Expedient.

Sensitive client credentials were stored in a secure password management system, and some credentials required approval and justification before access was granted.

The technology differs, but the security principles are very similar:

* Sensitive credentials should be protected
* Access should be restricted
* Privileged actions should be auditable

---

### Why This Matters

Key Vault is a core Azure security service used to prevent credentials from being stored in plaintext inside scripts, applications, or configuration files.

Understanding Key Vault also reinforces broader cloud security concepts such as RBAC, least privilege, and secure credential management.

## 2026-06-17 — Key Vault & Managed Identity

### What Was Built

Azure Key Vault was deployed to support secure secret storage for the environment.

A test secret (`sql-admin-password`) was created after resolving initial RBAC restrictions.

System-assigned Managed Identity was enabled on `vm-operationslab-linux01`, allowing the VM to authenticate to Azure services without storing credentials locally.

The VM’s identity was granted the **Key Vault Secrets User** role, completing the access path between the VM and Key Vault.

---

### Key Observations

Secret creation initially failed with a **Forbidden (RBAC)** error.

This highlighted a core Azure concept:

* **Control-plane access** — managing the Key Vault resource
* **Data-plane access** — reading and writing secrets

Permission to deploy and manage a Key Vault does not automatically grant access to the secrets stored inside it.

Assigning the **Key Vault Secrets Officer** role resolved the issue and allowed secret creation to proceed normally.

---

### What Was Learned

* Managed Identity provides an Azure-issued identity but does not grant permissions by itself.
* RBAC determines what that identity can access.
* Key Vault enforces strict separation between resource management and secret access.
* Authentication (identity) and authorization (permissions) are separate steps in Azure’s security model.
* The end-to-end flow between VM → Managed Identity → RBAC → Key Vault became much clearer through this configuration.

Access flow:

VM
↓
Managed Identity proves identity
↓
RBAC checks permissions
↓
Key Vault allows or denies access
↓
Secret returned if authorized

An important takeaway was understanding that assigning permissions does not automatically cause the VM to retrieve secrets. Something running on the VM, such as a script or application, must actively request access to Key Vault.

---

### Real-World Connection

This setup resembles privileged password systems used in traditional infrastructure environments.

Access to sensitive credentials is controlled, audited, and restricted, similar to the password vault processes used at Expedient.

Azure’s approach automates this through identities and tokens instead of manual credential retrieval.

Managed Identity also feels similar to service accounts or machine trust relationships used in traditional infrastructure.

---

### Challenges & Resolution

**Issue:** Secret creation blocked by RBAC
**Cause:** Missing data-plane permissions

**Resolution:**

* Verified Key Vault deployment
* Reviewed IAM permissions
* Identified missing role assignment
* Assigned **Key Vault Secrets Officer** role
* Allowed time for RBAC propagation

**Outcome:** Secret creation succeeded, and the VM now has the required permissions to access secrets in Key Vault.

---

### Why This Matters

This configuration reflects common production patterns where applications and virtual machines retrieve secrets securely without storing credentials locally.

This phase reinforced several important Azure administration concepts:

* Identity
* RBAC
* Least privilege
* Secret management
* Authentication vs authorization

This was one of the strongest examples so far of how Azure security concepts map to real-world infrastructure workflows.


The biggest takeaway for me was realizing that many Azure security concepts are not completely new—they often map back to security workflows I have already seen in enterprise IT.

## 2026-06-18 — Azure SQL Deployment

### Focus

Deploy Azure SQL Database to complete Phase 2 (Security & Identity) and add a managed database service to the environment.

### What Was Built

Azure SQL Database was deployed using the Basic pricing tier to provide a low-cost managed relational database for the lab environment.

Resources deployed:

* SQL Database: `sqldb-operationslab-dev`
* Logical SQL Server: `sql-operationslab-jarrod`

Configuration used:

* Pricing Tier: Basic (5 DTUs)
* Storage: 2 GB
* Connectivity: Public endpoint
* Allow Azure services: Disabled
* Minimum TLS Version: 1.2

### Key Observations

Azure SQL deployment creates two separate components:

* **Logical SQL Server** — manages authentication, firewall rules, connectivity, and administrative access
* **SQL Database** — stores the actual tables, rows, and application data

This reinforced an important PaaS concept:

Azure manages the underlying infrastructure, operating system, patching, and availability, while administrative focus stays on database configuration, access, and security.

Unlike traditional infrastructure, there is no VM or operating system to manage directly.

### What Was Learned

* Azure SQL is a Platform as a Service (PaaS) offering.
* The SQL server in Azure is a logical management layer, not a traditional server.
* Network access is controlled through firewall and endpoint configuration.
* Public endpoints can be used for lab testing while still restricting access through firewall rules.
* TLS is enforced to secure database connections.

### Challenges & Resolution

**Issue:** East US deployment was unavailable for the selected SQL server configuration.

**Cause:** Subscription or regional capacity limitations.

**Resolution:** SQL was deployed in West US using the lowest-cost Basic tier.

**Outcome:** Deployment succeeded and Phase 2 progress continued despite regional constraints.

### Real-World Connection

This introduced cloud database administration concepts that differ from traditional server administration.

Instead of managing operating systems, patching, or database server hardware, administration focuses more on:

* access control
* connectivity
* security
* cost management
* service configuration

This aligns with cloud operations work where infrastructure management shifts toward service management.

### Why This Matters

Azure SQL completes the core Phase 2 architecture by adding a managed database service to the environment.

Current architecture:

VM
↓
Managed Identity
↓
RBAC
↓
Key Vault
↓
Secret Storage

* Azure SQL Database

This expands the lab from core infrastructure into a more realistic cloud application environment involving compute, identity, secrets, and data services.

## 2026-06-19 — Monitoring & Alerting

### Focus

Begin Phase 3 (Monitoring & Operations) by reviewing cost usage and creating the first Azure Monitor alert rule.

### What Was Built

Cost analysis was reviewed after deploying Azure SQL to confirm the environment remained within budget.

Current cost status:

* Actual cost: $1.12
* Forecast: $2.37
* Budget: $3.00

No unexpected cost spike was observed after SQL deployment.

The first Azure Monitor alert rule was created for `vm-operationslab-linux01`.

Alert configuration:

* Signal: Percentage CPU
* Threshold: Average CPU > 80%
* Evaluation Frequency: 1 minute
* Lookback Period: 5 minutes

An Action Group was also created to send email notifications when the alert is triggered.

### Key Observations

Azure alerting is built around three core components:

* Metric
* Condition
* Evaluation Window

These components determine what is monitored, when an alert triggers, and how often Azure evaluates the resource.

Action Groups define what happens after an alert fires, such as email notifications or automation.

### What Was Learned

* Azure Monitor can evaluate resource metrics on a recurring schedule.
* Alert rules use thresholds and evaluation windows to detect abnormal behavior.
* Action Groups control alert notifications and response actions.
* Effective alerting requires balancing sensitivity with alert noise.

### Real-World Connection

This closely mirrors monitoring workflows used at Expedient.

High CPU usage alerts were common and typically required checking which process or service was consuming resources.

Not every alert indicated a problem. In some cases, high CPU usage was expected based on workload, which required adjusting thresholds or evaluation windows to reduce unnecessary alert noise.

The operational workflow feels very similar:

Monitoring platform → Alert → Investigation → Escalation or Tuning

The primary difference is the platform, with Azure Monitor replacing traditional infrastructure monitoring tools such as VMware vSphere.

### Why This Matters

Monitoring and alerting are core cloud operations responsibilities.

This marks the start of Phase 3 and expands the project beyond infrastructure deployment into proactive operational monitoring and incident response.

## 2026-06-21 — Azure Monitor Disk Alert & Cost Review

### Focus

Expanded VM monitoring and reviewed current Azure costs.

### What Was Built

Azure Monitor alerting was expanded by creating a second VM metric alert for disk performance.

**New alert created:**

* **OS Disk IOPS Alert** (`alert-vm-osdisk-high`)

**Configuration:**

* Signal: **OS Disk IOPS Consumed Percentage**
* Threshold: **Greater than 90%**
* Aggregation: **Average**
* Evaluation Frequency: **Every 1 minute**
* Lookback Period: **5 minutes**
* Severity: **Sev 2 — Warning**

The alert was connected to the existing Action Group:

* **ag-vm-alerts**

This allows email notifications when the alert condition is triggered.

### Key Observations

CPU and disk alerts monitor different types of infrastructure bottlenecks.

* **CPU alerts** help identify compute pressure caused by heavy processing or runaway workloads.
* **Disk IOPS alerts** help identify storage bottlenecks caused by high read/write activity.

High disk IOPS does **not** indicate low disk space.

Instead, it measures how heavily the disk is being used for read/write operations.

Examples of workloads that may increase disk IOPS:

* Database activity
* Backup operations
* Log processing
* High read/write workloads

### What Was Learned

* Azure Monitor supports metric-based alerting for VM performance.
* Multiple alerts can reuse the same Action Group for centralized notifications.
* CPU and disk pressure represent different performance issues and should be monitored separately.
* Alert thresholds should balance early warning with reducing unnecessary alert noise.

Typical response workflow:

1. Alert triggers
2. Metrics are reviewed
3. Root cause is investigated
4. Decision is made to remediate, escalate, or adjust thresholds

### Cost Review

Azure cost analysis was reviewed before continuing project work.

**Current cost:**

* **Actual Cost:** $1.69
* **Forecasted Monthly Cost:** $2.86
* **Budget:** $3.00

**Primary cost contributors:**

* Virtual Network: **$0.92**
* Storage: **$0.39**
* SQL Database: **$0.38**

**Observations:**

* SQL costs increased compared to the previous review, indicating billing had continued catching up after deployment.
* Virtual networking remains the largest cost contributor.
* Metric alert pricing remains low at approximately **$0.10/month per alert**.

Current costs remain within budget and do not require changes.

### Real-World Connection

This monitoring workflow closely resembles infrastructure alert handling at Expedient.

High CPU and disk alerts typically involved:

* Reviewing performance metrics
* Identifying the process or workload causing resource pressure
* Determining whether action or threshold adjustments were needed

The same operational workflow applies in Azure using Azure Monitor and metric alerts.

### Why This Matters

The environment now includes proactive alerting for two core infrastructure performance areas:

* CPU utilization
* Disk I/O utilization

This improves visibility into system health and better reflects real-world cloud operations practices.

2026-06-29 — Activity Logs & Log Analytics Integration

**Focus**

Continue Phase 3 (Monitoring & Operations) by reviewing Azure costs after recent infrastructure changes and validating centralized log collection in Log Analytics.

**What Was Built**

Azure cost analysis was reviewed after removing the VM Public IP to determine whether networking costs had changed.

Current cost status:

* Actual Cost: $4.38
* Forecasted Monthly Cost: $4.64
* Budget: $3.00

Primary cost contributors:

* Virtual Network: $1.89
* SQL Database: $1.68
* Storage: $0.81

Observations from cost review:

* Public IP no longer appeared in the cost breakdown, confirming deletion succeeded.
* VM compute cost showed as $0.00 because the VM was deallocated from auto-shutdown.
* Azure SQL had become one of the largest recurring costs in the environment.

After cost review, Log Analytics Workspace was investigated because queries were returning no results.

Initial queries against `AzureActivity` returned no data.

Further investigation showed Azure Activity Logs did exist at the subscription level, but they were not being forwarded into the Log Analytics Workspace.

To resolve this, a Diagnostic Setting was created:

* Diagnostic Setting: `diag-activitylogs-law`
* Destination: `law-operationslab-dev`

Enabled Activity Log categories:

* Administrative
* Security
* ServiceHealth
* Alert
* Recommendation
* Policy
* Autoscale
* ResourceHealth

After configuration, the VM was started and stopped to generate fresh activity events for testing.

Log ingestion was later validated in Log Analytics using the `AzureActivity` table.

**Key Observations**

Azure Activity Logs and Log Analytics are separate components.

Azure was already recording management events such as:

* VM start and stop
* Alert creation
* Resource changes
* Diagnostic setting updates

However, those logs were not visible inside Log Analytics until Diagnostic Settings were configured.

This reinforced the monitoring pipeline:

Azure Resource / Subscription
↓
Activity Logs Generated
↓
Diagnostic Settings
↓
Log Analytics Workspace
↓
Query / Analysis

**What Was Learned**

* Log Analytics Workspace does not automatically collect Azure logs.
* Diagnostic Settings are required to route subscription or resource logs into Log Analytics.
* VM compute charges stop when a VM is deallocated, but persistent resources continue billing.
* Managed services such as Azure SQL can become major recurring cost drivers even in small environments.

KQL queries were used to validate log ingestion, but this session focused more on understanding log flow and monitoring architecture than learning KQL itself.

**Challenges & Resolution**

**Issue 1:** Budget deletion initially failed with a portal error.

**Cause:** Azure portal caching / stale UI state.

**Resolution:** Refreshing the page confirmed the budget had already been deleted successfully.

**Issue 2:** Log Analytics queries returned no results.

**Cause:** Activity Logs existed, but no Diagnostic Settings were configured to forward them to Log Analytics.

**Resolution:**

* Verified Activity Logs existed in Azure Monitor
* Created subscription-level Diagnostic Settings
* Routed logs to `law-operationslab-dev`
* Waited for ingestion to complete
* Confirmed logs appeared in Log Analytics

**Outcome:** Centralized activity logging is now functioning correctly.

**Real-World Connection**

This session closely reflected real infrastructure troubleshooting.

At Expedient, monitoring issues were not always caused by missing alerts. In many cases, the issue was determining whether the right monitoring data was reaching the right tools for investigation.

The same operational concept applies in Azure.

Monitoring is not only about generating alerts or logs — it also requires ensuring telemetry is properly collected and accessible for analysis.

**Why This Matters**

This expands Phase 3 beyond metric-based alerting into centralized operational logging.

The environment now includes:

* CPU alerting
* Disk IOPS alerting
* Email notifications through Action Groups
* Centralized Activity Log collection in Log Analytics

This better reflects real-world cloud operations where administrators need both proactive alerts and historical log data for investigation and troubleshooting.
