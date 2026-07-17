# Azure Operations Lab

A hands-on Azure project focused on building practical cloud administration skills through real-world operational scenarios, including monitoring, security, recovery, troubleshooting, and infrastructure management.

## Project Status

**Current Phase:** Operations & Administration

The foundational Azure infrastructure has been deployed. Current work focuses on operating and maintaining the environment through monitoring, recovery, security, troubleshooting, and documentation. New resources are added only when they support a realistic operational scenario.

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

### Azure Administration

- Resource Groups
- Azure Storage
- Virtual Networks
- Network Security Groups
- Virtual Machines
- Azure SQL Database

### Identity & Security

- Azure Key Vault
- Managed Identity
- Azure RBAC

### Monitoring & Operations

- Azure Monitor
- Log Analytics
- Alerts
- Cost Management

### Automation

- PowerShell
- Bicep

---

## Current Status

### Current Phase Summary

* Phase 1 — Foundation: Completed
* Phase 2 — Security & Identity: Completed
* Phase 3 — Monitoring & Operations: Completed
* Phase 4 — Operations & Recovery: In Progress
* Phase 5 — Advanced Networking & Security: Planned

---

### Current Focus

The project has transitioned into an operations-focused environment.

Current work emphasizes:

- Recovery
- Troubleshooting
- Security validation
- Operational maintenance
- Cost management
- Documentation

### Planned

- Key Vault Secret Rotation
- VM Connectivity Troubleshooting
- Network Security Group Validation
- RBAC Validation
- Additional SQL recovery scenarios
- Resource cleanup

---

## Current Issues

* App Service deployment is paused due to a Microsoft.Web/serverFarms subscription/quota-related validation error
* Enhanced VM monitoring (Azure Monitor Agent / Data Collection Rules) was investigated but deferred due to additional complexity and cost considerations
* Azure SQL deployment in East US was unavailable due to subscription or regional capacity limitations, so SQL was deployed in West US

These issues do not currently block project progress.

---

## Roadmap

### Current

- Key Vault Secret Rotation
- Azure Cost Review

### Upcoming

- VM Connectivity Troubleshooting
- Network Security Group Validation
- RBAC Validation
- Additional SQL recovery scenarios
- Resource Cleanup

---

## Repository Documentation

This repository includes three primary documents.

### README.md

High-level overview of project goals, current progress, and technologies used.

### architecture.md

Documents the overall environment design, resource relationships, and phased roadmap.

### project-journal.md

Tracks deployment progress, technical observations, troubleshooting, real-world connections, and key lessons learned throughout the project.
