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

## 2026-06-30 — Azure SQL Monitoring Exploration

### Focus

Continue Phase 3 (Monitoring & Operations) by exploring Azure SQL monitoring and understanding how monitoring a managed database differs from monitoring a virtual machine.

### What Was Built

Azure SQL metrics were explored for the following resources:

* **SQL Database:** `sqldb-operationslab-dev`
* **Logical SQL Server:** `sql-operationslab-jarrod`

The **Metrics** blade was used to review available monitoring signals for the SQL database.

**Available SQL metrics included:**

* CPU percentage
* Data IO percentage
* Data space allocated
* Data space used
* Data space used percent
* Deadlocks
* DTU Limit
* Firewall-related metrics

Three metrics were examined in detail.

**CPU Percentage**

Observed peak:

* **~0.0043%**

CPU usage remained effectively idle, indicating the database currently has almost no active workload.

**Data Space Used**

Observed usage:

* **~22.3 MB used**

Storage usage showed slow gradual growth over time, with no indication of storage pressure.

**Deadlocks**

Observed value:

* **0**

No transaction conflicts were detected.

### Key Observations

Azure SQL monitoring differs significantly from VM monitoring.

VM monitoring primarily focuses on infrastructure health such as:

* CPU utilization
* Disk I/O
* Memory pressure
* Network usage

Azure SQL monitoring focuses more on service and workload behavior such as:

* Query workload
* Storage growth
* Transaction contention
* Database throughput

This reflects the difference between **IaaS** and **PaaS** administration.

With Azure SQL, Azure manages the operating system, patching, and underlying infrastructure, shifting administrative focus toward service performance and capacity.

### What Was Learned

* Azure SQL exposes workload-focused metrics instead of traditional operating system metrics.
* DTU represents a bundled performance measurement combining compute, memory, and storage I/O capacity.
* CPU metrics help identify workload pressure on the database.
* Storage metrics help track database growth and capacity usage.
* Deadlocks help identify transaction contention and concurrency issues.

A deadlock occurs when multiple transactions wait on each other indefinitely, requiring SQL to terminate one transaction to resolve the conflict.

### Real-World Connection

This monitoring workflow felt very similar to infrastructure monitoring work performed at Expedient.

Typical workflow:

1. Resource is reviewed
2. Metrics are analyzed
3. Time range is adjusted if needed
4. Behavior is evaluated as normal or abnormal
5. Further investigation is performed if necessary

Although Azure uses different tooling, the operational mindset remains very similar.

The same troubleshooting habits apply:

* Reviewing metrics
* Identifying spikes or trends
* Determining expected vs unexpected behavior
* Deciding whether action is needed

This reinforced that many cloud operations skills build on traditional infrastructure monitoring experience.

### Why This Matters

This session expanded Phase 3 beyond VM monitoring into managed service monitoring.

The project now includes monitoring exposure across both:

* Infrastructure resources (VM)
* Platform services (Azure SQL)

This improves understanding of how monitoring responsibilities change when moving from infrastructure administration to cloud service administration.

The next step is implementing SQL alerting to move from passive metric review into proactive monitoring.

## 2026-07-07 — Azure SQL Storage Alert

### Focus

Expanded Azure Monitor by creating the first alert rule for Azure SQL Database storage utilization.

### What Was Built

A metric alert was created to monitor Azure SQL Database storage usage.

**New alert created:**

* **SQL Data Space Alert** (`alert-sql-dataspace-high`)

**Configuration:**

* Signal: **Data space used percent**
* Threshold: **Greater than 80%**
* Aggregation: **Maximum**
* Evaluation Frequency: **Every 1 minute**
* Lookback Period: **5 minutes**
* Severity: **Sev 2 — Warning**

The alert was connected to the existing Action Group:

* **ag-vm-alerts**

This allows email notifications to be reused across multiple Azure resources.

### Key Observations

Azure SQL Database alerting uses the same Azure Monitor workflow as VM alerting, but the signals are different.

VM alerts focus on infrastructure metrics such as:

* CPU utilization
* Disk I/O
* Network activity

SQL Database alerts focus more on managed database metrics such as:

* Storage utilization
* DTU usage
* CPU percentage
* Deadlocks
* Failed connections

The database was currently using about **1%** of its allocated data space, so the alert is not expected to trigger during normal lab activity.

### What Was Learned

* Azure SQL Database supports metric-based alerting through Azure Monitor.
* Existing Action Groups can be reused across different Azure resources.
* **Data space used percent** is useful for tracking database capacity usage.
* Alert thresholds should provide early warning before storage usage becomes a problem.
* Monitoring a managed SQL database focuses more on service health and capacity than operating system performance.

### Real-World Connection

This monitoring workflow connects to infrastructure monitoring work performed at Expedient.

At Expedient, high resource usage alerts required reviewing metrics, checking time ranges, and determining whether the behavior was expected or needed action.

The same operational workflow applies in Azure:

1. Alert triggers
2. Metrics are reviewed
3. Behavior is investigated
4. Decision is made to remediate, escalate, or adjust thresholds

The tools are different, but the monitoring process is familiar.

### Why This Matters

The environment now includes proactive alerting across both infrastructure and platform services.

Current monitored resources include:

* Virtual Machine CPU utilization
* Virtual Machine Disk I/O utilization
* Azure SQL Database storage utilization

This expands Phase 3 by adding database capacity monitoring and better reflects real-world cloud operations practices.

## 2026-07-11 — Azure SQL Query Editor & Monitoring Validation

### Focus

Validated Azure SQL Database functionality by creating a sample table, inserting data, and confirming Azure Monitor captured live database workload.

### What Was Built

Connected to the Azure SQL Database using the Azure Portal Query Editor.

An initial connection attempt was blocked because the SQL Server firewall did not allow the current public IP address. Azure automatically prompted to add the firewall rule, allowing the connection without manually configuring the SQL Server.

**Database objects created:**

* **Employees** table

**Table Structure**

* **EmployeeID** (Primary Key)
* **FirstName**
* **LastName**
* **Department**

**Sample records inserted:**

| EmployeeID | First Name | Last Name | Department |
|------------|------------|-----------|------------|
| 1 | Jarrod | Mills | IT |
| 2 | Jane | Smith | HR |
| 3 | Mike | Johnson | Accounting |

The table was then queried successfully using a `SELECT` statement to verify the data had been written correctly.

### Key Observations

Prior to generating database activity, Azure Monitor showed little or no DTU utilization.

After creating the table, inserting records, and querying the data, Azure Monitor recorded a measurable workload.

**Observed metrics:**

* **DTU Percentage:** peaked at approximately **1%**
* Database storage increased slightly as records were added.
* Azure Monitor successfully captured the workload shortly after the queries completed.

Although the workload was very small, it demonstrated that Azure SQL metrics update in response to actual database activity.

### What Was Learned

* Azure SQL Query Editor allows basic database administration directly from the Azure Portal.
* SQL Server firewall rules must allow the client's public IP before browser-based connections are permitted.
* Azure can automatically create the required firewall rule directly from the Query Editor login screen.
* Creating tables, inserting data, and running queries immediately generate measurable Azure Monitor metrics.
* **DTU Percentage** measures database workload rather than database storage usage.

Typical operational workflow:

1. Connect to the database.
2. Execute SQL queries.
3. Azure Monitor collects workload metrics.
4. Review performance trends.
5. Investigate unexpected activity if resource utilization appears abnormal.

### Real-World Connection

This workflow closely mirrors infrastructure monitoring performed at Expedient.

Rather than monitoring for constant high utilization, the focus was identifying workload changes and investigating what generated them.

The same operational workflow applies in Azure:

1. Database activity occurs.
2. Azure Monitor records performance metrics.
3. Metrics are reviewed.
4. Resource utilization is correlated with recent activity.
5. Decision is made to investigate, remediate, or continue monitoring.

Although Azure SQL is a managed platform service, the operational monitoring process is very similar to monitoring traditional infrastructure.

### Why This Matters

The Azure SQL environment has now been validated beyond simple deployment.

Current SQL capabilities include:

* Browser-based SQL administration
* Database object creation
* Data insertion
* Data retrieval using SQL queries
* Live workload monitoring through Azure Monitor
* Validation that Azure Monitor captures real database activity

This expands Phase 3 by demonstrating both operational database management and real-time performance monitoring, providing hands-on experience that closely resembles production cloud operations.

## 2026-07-12 — Azure SQL Database Fundamentals

### Focus

Built foundational Azure SQL Database skills by creating and managing relational data, supporting common cloud administration tasks such as validating records, troubleshooting application data, and understanding how managed database services are operated.

### What Was Built

Connected to the Azure SQL Database through the Azure Portal Query Editor and created a simple `Employees` table.

**Table created:**

* **Employees**

**Columns:**

* EmployeeID (Primary Key)
* FirstName
* LastName
* Department

Sample employee records were added to simulate a small production database.

### Tasks Completed

Practiced the four core database operations (CRUD) used when working with relational databases.

**Create**

* Created the `Employees` table.

**Insert**

* Added three employee records.

**Read**

* Retrieved employee information using `SELECT` statements.

**Update**

* Updated EmployeeID 1 from **IT** to **Cloud Operations**.

**Delete**

* Removed EmployeeID 2 from the database.

Each change was verified by querying the database after the operation completed.

### Query Practice

Practiced retrieving information using common SQL queries that administrators frequently use during troubleshooting.

**Queries performed:**

* Display all employees.
* Retrieve a single employee using `WHERE`.
* Filter employees by department.
* Return only selected columns.
* Sort records alphabetically using `ORDER BY`.
* Count total employees using `COUNT(*)`.
* Count employees within a specific department.

These exercises demonstrate how administrators locate and verify information without modifying the underlying data.

### Key Observations

Although Azure SQL Database is a managed Platform-as-a-Service (PaaS) offering, database administration still relies on many of the same operational concepts found in traditional SQL environments.

Most day-to-day operational work involves retrieving and validating information rather than designing databases.

Filtering, sorting, counting records, and verifying changes are common administrative tasks during troubleshooting and application support.

### Challenges & Resolution

* Azure SQL Query Editor initially blocked access because the client IP address was not allowed by the SQL Server firewall.
* Added the current public IP address through the Azure Portal and successfully established a connection.
* Accidentally attempted to create the `Employees` table twice, resulting in an "object already exists" error.
* Verified the table had already been created and continued with the remaining CRUD operations.
* SQL performance metrics did not initially appear after creating the database. After executing queries against the database, Azure Monitor began collecting activity and the DTU metric became visible.

### What Was Learned

* Azure SQL Database can be managed directly through the Azure Portal Query Editor.
* SQL databases organize information into tables containing rows and columns.
* CRUD (Create, Read, Update, Delete) operations form the foundation of relational database management.
* `SELECT`, `WHERE`, `ORDER BY`, and `COUNT` are among the most commonly used SQL statements for operational work.
* Database changes should always be verified after execution.
* Azure Monitor only displays meaningful SQL performance metrics after the database begins processing workload.

### Real-World Connection

This lab reflects many of the database interactions performed by infrastructure and cloud administrators.

In production environments, administrators frequently query databases to verify user records, confirm configuration changes, troubleshoot application issues, and validate automation tasks.

While developers design applications that use databases, operations teams often focus on reading, validating, and maintaining the underlying data.

The workflow closely mirrors operational troubleshooting:

1. Connect to the database.
2. Retrieve the necessary information.
3. Verify the current state.
4. Make changes if required.
5. Confirm the changes were applied successfully.

This approach is similar to support work performed at Expedient, where investigating alerts or application issues often involved validating data, confirming system state, and determining whether corrective action was necessary.

### Learning Rule

Reading documentation introduces concepts, but executing SQL queries and verifying the results builds operational confidence. Hands-on repetition is what turns knowledge into practical troubleshooting skills.

### Why This Matters

This lab introduces practical SQL skills that support cloud infrastructure administration without focusing on software development.

Current Azure SQL experience now includes:

* Connecting through the Azure Portal Query Editor.
* Managing SQL Server firewall access.
* Creating relational database tables.
* Performing CRUD operations.
* Retrieving data using common SQL queries.
* Filtering, sorting, and counting records.
* Verifying changes after database operations.
* Observing Azure Monitor collect performance metrics after database activity.

## 2026-07-13 — Azure SQL Monitoring Validation and Basic Database Operations

### Focus

Built foundational SQL skills while validating Azure SQL Database monitoring through Azure Monitor. The session focused on performing basic database operations, verifying that Azure Monitor collected workload metrics, and confirming that monitoring was functioning as expected.

### What Was Built

Performed basic SQL CRUD (Create, Read, Update, Delete) operations using the Azure SQL Database Query Editor.

**SQL operations completed:**

* Created an `Employees` table.
* Inserted sample employee records.
* Queried the table using `SELECT`.
* Updated an employee's department.
* Deleted a sample employee record.
* Verified all changes using additional `SELECT` queries.

Reviewed the previously created Azure SQL storage alert and confirmed:

* **SQL Data Space Alert** (`alert-sql-dataspace-high`)
* Action Group: **ag-vm-alerts**
* Alert configuration remained healthy and enabled.

Validated Azure Monitor metrics by reviewing:

* DTU Percentage
* CPU Percentage

### Monitoring Validation

Database activity generated during the SQL exercises appeared in Azure Monitor after selecting the appropriate time range.

Key observations included:

* Azure Monitor successfully collected SQL workload metrics.
* The default **24-hour** view did not initially display the activity.
* Changing the time range to **7 Days** displayed the database workload.
* Both **DTU Percentage** and **CPU Percentage** showed a brief spike of approximately **1%** while SQL queries were executing before returning to near 0%.

This confirmed that Azure Monitor was successfully collecting performance data for the Azure SQL Database.

### Key Observations

Azure SQL Database exposes operational metrics similar to those used for monitoring virtual machines, but the focus is different.

Examples include:

* DTU Percentage
* CPU Percentage
* Storage Utilization
* Data Space Used Percentage

Unlike traditional SQL Server administration, Azure SQL monitoring emphasizes managed service health and resource consumption rather than operating system performance.

The session also reinforced that Azure Monitor visualizations depend on the selected time range, making it important to verify historical windows when expected activity is not immediately visible.

### Challenges & Resolution

**Challenge:**

Initially, no database activity appeared in Azure Monitor after executing SQL queries.

**Resolution:**

The issue was not with data collection. Expanding the chart from the default **24-hour** view to **7 Days** revealed the recorded workload, confirming that Azure Monitor had successfully captured the database activity.

### What Was Learned

* Azure SQL Database supports browser-based administration through the Query Editor.
* Basic SQL operations can be performed directly within the Azure portal.
* Azure Monitor automatically captures database workload metrics.
* DTU Percentage and CPU Percentage provide insight into database resource utilization.
* Time range selection is an important part of validating monitoring data.

### Real-World Connection

This session closely relates to operational work performed at Expedient.

Although Expedient primarily supported traditional server infrastructure, troubleshooting often began by reviewing monitoring data before taking corrective action.

The same operational workflow applies in Azure:

1. Generate or observe workload.
2. Review monitoring data.
3. Verify expected system behavior.
4. Determine whether action is required.

While Azure SQL is a managed platform service, the overall monitoring process follows the same operational mindset.

### Why This Matters

The Operations Lab now includes both infrastructure monitoring and managed database monitoring.

Current monitoring coverage includes:

* Virtual Machine CPU utilization
* Virtual Machine Disk I/O utilization
* Azure SQL Database storage utilization
* Azure SQL Database DTU utilization
* Azure SQL Database CPU utilization

This expands the monitoring capabilities of the lab and provides hands-on experience with validating cloud resource performance using Azure Monitor.

### Learning Rule

Monitoring data is only valuable if it is interpreted correctly. Before assuming data is missing or a service is not working, verify configuration details such as the selected time range, metric, and aggregation settings.

## 2026-07-15 — Azure SQL Administration Exploration

### Focus

Expanded Azure SQL administration skills by reviewing monitoring data, validating alert configuration, exploring recovery capabilities, and examining the operational properties used to verify and troubleshoot a managed SQL database.

### What Was Built

No new Azure resources were deployed during this session.

Instead, time was spent exploring and validating existing Azure SQL Database functionality to better understand how an administrator manages an existing database.

Areas explored included:

- Azure SQL Metrics
- Existing Azure Monitor Alert Rule
- Point-in-Time Restore
- Database Properties
- SQL CRUD operation review

### Configuration Reviewed

#### Azure Monitor Metrics

Reviewed multiple Azure SQL performance metrics, including:

- **DTU Percentage**
- **CPU Percentage**

Both metrics showed approximately **1% utilization**, reflecting the light workload generated by the lab.

Changing the Metrics time range from **Last 24 Hours** to **Last 7 Days** displayed the previous SQL activity, confirming that Azure Monitor had successfully collected performance data.

#### Alert Rule Validation

Reviewed the existing SQL storage alert.

**Alert Configuration:**

- Alert Name: **alert-sql-dataspace-high**
- Signal: **Data Space Used Percent**
- Threshold: **Greater than 80%**
- Severity: **Sev 2 — Warning**
- Action Group: **ag-vm-alerts**

The alert configuration was validated without making changes.

Previous testing had already confirmed that the Action Group successfully sends email notifications.

#### Point-in-Time Restore

Explored Azure SQL Database restore options.

Observed that Azure automatically creates restore points after deployment, allowing administrators to restore a database to an earlier point in time without manually creating backups.

No restore operation was performed since the lab database is actively being used.

#### Database Properties

Reviewed the database Properties page to identify information commonly referenced during administration and troubleshooting.

Properties reviewed included:

- Database Status
- Pricing Tier
- Maximum Storage
- Server Name
- Location
- Creation Date
- SQL Administrator Login
- Resource Group
- Connection Information
- Resource ID

The **Microsoft Entra Administrator** field was noted as **Not Configured**, which matches the current lab design using SQL authentication.

### Key Observations

- Azure Monitor stores historical SQL performance data even when utilization is very low.
- Selecting an appropriate time range is important when reviewing historical metrics.
- Azure SQL automatically maintains restore points for Point-in-Time Recovery.
- The Properties page provides a centralized location for validating database configuration and deployment details.
- Existing monitoring and alerting configuration continued functioning without requiring additional changes.

### What Was Learned

- Azure SQL metrics can be reviewed directly through Azure Monitor to evaluate database activity over time.
- Historical metric data may require expanding the time range to view previous activity.
- Azure SQL provides automatic Point-in-Time Recovery through managed backups.
- Database Properties provide valuable operational information used during troubleshooting and documentation.
- Existing Azure Monitor alerts can be reviewed and validated without modifying their configuration.

### Real-World Connection

This session closely mirrors day-to-day administrative work.

Rather than deploying new resources, administrators frequently spend time validating existing infrastructure by:

1. Reviewing performance metrics.
2. Confirming alert configurations.
3. Verifying recovery capabilities.
4. Checking resource properties.
5. Ensuring deployed services match documented configurations.

These validation activities help identify configuration issues before they become production problems.

### Challenges & Resolution

**Challenge**

Initially, SQL metrics appeared to contain no activity.

**Resolution**

The Metrics blade was displaying only the previous 24 hours of data. Expanding the time range to the previous seven days revealed the SQL activity generated during earlier lab exercises, confirming that Azure Monitor had successfully collected the performance data.

### Why This Matters

This session strengthened operational familiarity with Azure SQL Database administration by focusing on validation rather than deployment.

The Operations Lab now includes practical experience with:

- SQL data management
- Azure Monitor metrics
- Azure SQL alert validation
- Automatic recovery capabilities
- Database property verification

These activities closely reflect the routine operational checks performed by cloud administrators.

### Learning Rule

Building a cloud resource is only the beginning.

Effective administration also requires validating configuration, monitoring performance, understanding recovery options, and knowing where to find operational information when troubleshooting.
