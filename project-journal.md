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
