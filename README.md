Azure Operations Lab
Purpose

This project is a hands-on Azure environment designed to demonstrate real-world cloud administration skills. It focuses on infrastructure, networking, identity, monitoring, and automation — the core responsibilities of Azure Administrator, Systems Administrator, Infrastructure Engineer, and Cloud Operations roles.

The project was created to gain practical Azure experience outside of my day-to-day IT Analyst responsibilities and to build a portfolio that demonstrates cloud administration skills.
Project Goals

    Build a complete Azure environment

    Practice Azure administration using real services

    Demonstrate networking, identity, security, monitoring, and automation

    Document the environment clearly for GitHub and interview discussions

Non-Goals

This project intentionally avoids:

    Advanced software development

    Complex web applications

    AI/ML workloads

    Kubernetes

    Large enterprise-scale architectures

Skills Demonstrated

    Resource Groups

    Virtual Networks

    Network Security Groups

    App Service

    Azure SQL Database

    Key Vault

    Managed Identity

    Azure Monitor

    Log Analytics

    Alerts

    PowerShell

    Bicep

Current Status

Phase 1 – Planning

Next Step:
Define the initial architecture and Phase 1 resources.
Phase 1 — Core Resources
Overview

This project is a hands‑on Azure environment designed to strengthen real‑world administration skills and prepare for AZ‑104 and M365 admin roles. The goal is to build a realistic, enterprise‑style environment without unnecessary complexity.
Skills Demonstrated

    Resource Groups

    Storage Accounts

    Log Analytics Workspace

    Diagnostic Settings (metrics)

    Azure Portal navigation

    Documentation and project structure

Phase 1 Resources Deployed

Resource Group  
rg‑operationslab‑dev created as the logical container for all project resources.

Storage Account  
stoperationslab01 deployed with:

    Standard performance

    Locally redundant storage (LRS)

    General Purpose v2

    Soft delete enabled for blobs and containers

    Public network access enabled (default)

Log Analytics Workspace  
law‑operationslab‑dev created to support monitoring, logging, and future VM insights.
Monitoring Setup

Diagnostic settings were created at the Storage Account level for metrics.
Blob service logs will be configured later in the project when needed.
This does not block progress.
Project Approach

    Calm, steady pacing

    No overengineering

    Documentation that reflects real admin work

    Each phase builds toward a complete, interview‑ready environment
