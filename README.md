# Azure Operations Lab

## Project Status

**Current Phase:** Operations & Administration

The foundational Azure infrastructure has been deployed. Current work focuses on operating and maintaining the environment through monitoring, recovery, security, troubleshooting, and documentation. New resources are added only when they support a realistic operational scenario.

## Purpose

## Purpose

This project is a hands-on Azure Operations Lab designed to simulate the day-to-day responsibilities of a Junior Cloud Administrator, Systems Administrator, or Infrastructure Engineer.

Rather than focusing solely on deploying Azure resources, the project emphasizes operating, maintaining, monitoring, securing, recovering, and troubleshooting an existing Azure environment.

The goal is to gain practical Azure administration experience outside of day-to-day IT support responsibilities while building a portfolio that demonstrates production-style operational skills.
---

## Project Goals

* Build and operate a complete Azure environment
* Practice Azure administration using real services
* Demonstrate networking, identity, security, monitoring, and automation
* Document architecture, deployment decisions, troubleshooting, and lessons learned
* Create a project that supports resume and interview discussions
* Develop practical operational decision-making and troubleshooting experience

---

## Non-Goals

This project intentionally avoids:

* Advanced software development
* Complex web applications
* AI / ML workloads
* Kubernetes
* Large enterprise-scale architectures

The focus is practical Azure administration rather than software engineering.

---

## Skills Demonstrated

Azure Administration

• Resource Groups
• Azure Storage
• Virtual Networks
• Network Security Groups
• Virtual Machines
• Azure SQL Database

Identity & Security

• Azure Key Vault
• Managed Identity
• RBAC

Monitoring & Operations

• Azure Monitor
• Log Analytics
• Alerts
• Cost Management

Automation

• PowerShell
• Bicep

---

## Project Approach

This project follows a practical, step-by-step approach designed to build real Azure administration experience without unnecessary complexity.

Project principles:

* Stay practical
* No overengineering
* Build one meaningful resource or feature at a time
* Understand why before deploying anything
* Explore each resource after deployment
* Document what was learned
* Prioritize interview value over certification coverage

Documentation reflects real-world administrator work, including:

* Deployment decisions
* Troubleshooting
* Configuration choices
* Security considerations
* Operational lessons learned

Each phase moves the project closer to a complete, interview-ready Azure environment.

---

## Current Status

### Current Phase Summary

* Phase 1 — Foundation: Completed
* Phase 2 — Security & Identity: Completed
* Phase 3 — Monitoring & Operations: In Progress
* Phase 4 — Automation: Planned
* Phase 5 — Advanced Networking & Security: Planned

---

## Completed

### Phase 1 — Foundation

* GitHub repository created
* README created
* Project Journal created
* Architecture document created
* Resource Group deployed
* Storage Account deployed
* Log Analytics Workspace deployed
* Virtual Network deployed
* Network Security Group deployed and associated with subnet
* Linux Virtual Machine deployed
* Budget alerts configured
* VM auto-shutdown configured

### Phase 2 — Security & Identity

* Azure Key Vault deployed
* Test secret created (`sql-admin-password`)
* System Assigned Managed Identity enabled on VM
* RBAC configured between VM and Key Vault
* Azure SQL Database deployed (Basic tier)
* Logical SQL Server configured
* Public endpoint configured with restricted access

---

## Current Issues

* App Service deployment is paused due to a Microsoft.Web/serverFarms subscription/quota-related validation error
* Enhanced VM monitoring (Azure Monitor Agent / Data Collection Rules) was investigated but deferred due to additional complexity and cost considerations
* Azure SQL deployment in East US was unavailable due to subscription or regional capacity limitations, so SQL was deployed in West US

These issues do not currently block project progress.

---

## Next Step

### Phase 3 — Monitoring & Operations

Completed:

* Azure Monitor CPU alert created
* Azure Monitor OS Disk IOPS alert created
* Action Group configured for email notifications
* Alert notifications successfully validated
* Subscription Activity Logs exported to Log Analytics
* Log ingestion validated in Log Analytics Workspace
* Azure Activity Log integration configured
* Basic KQL queries used to validate Azure administrative activity
  
Planned:

* Additional VM monitoring
* SQL monitoring
* Additional diagnostic settings
* More log analysis scenarios

---

## Repository Documentation

This repository includes three primary documents.

### README.md

High-level overview of project goals, current progress, and technologies used.

### architecture.md

Documents the overall environment design, resource relationships, and phased roadmap.

### project-journal.md

Tracks deployment progress, technical observations, troubleshooting, real-world connections, and key lessons learned throughout the project.
