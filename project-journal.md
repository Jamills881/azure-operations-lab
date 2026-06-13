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



