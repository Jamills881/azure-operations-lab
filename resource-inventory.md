# Virtual Machine

## vm-operationslab-linux01

**Purpose**

Provides the primary compute resource for the environment and will host the project workload.

**Configuration**

- Ubuntu Linux
- East US
- Connected to subnet-main

**Connected Resources**

- Network Interface
- Public IP
- NSG
- Managed Identity
- Key Vault

**Monitoring**

- CPU Alert
- Disk Alert
- Log Analytics

**Notes**

Currently running and used for Azure administration exercises.

## Resource Group

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| rg-operationslab-dev | Resource Group | Active | Primary resource group containing the Azure Operations Lab resources. |

## Virtual Network

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| vnet-operationslab-dev | Virtual Network | Active | Provides network connectivity for the lab environment. |

## Virtual Machine

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| vm-operationslab-linux01 | Virtual Machine | Stopped (deallocated) | Linux VM used for administration, monitoring, and operational testing. |

## SQL Server

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| sql-operationslab-jarrod | SQL Server | Available | Hosts the lab databases. |

## SQL Database

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| sql-operationslab-jarrod | SQL Database | Online | Primary database for the project. |
| sql-operationslab-jarrod-restore-20260710 | SQL Database | Online | Database restored during point-in-time recovery testing. |

## Key Vault

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| kv-operationslab-jarrod | Key Vault | Active | Stores secrets used by the lab environment. |

## Storage Account

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| stoperationslab01 | Storage Account | Available | Stores project data and supports Azure services. |

## Log Analytics Workspace

| Name | Type | Status | Purpose |
|------|------|--------|---------|
| law-operationslab-dev | Log Analytics Workspace | Active | Central workspace for logs, monitoring, and queries. |

## Alert Rules

| Name | Target | Condition | Status |
|------|--------|-----------|--------|
| High CPU Alert - VM | Virtual Machine | CPU > 80% | Enabled |
| alert-vm-osdisk-high | Virtual Machine | OS Disk IOPS > 90% | Enabled |
| alert-sql-dataspace-high | SQL Database | Storage > 80% | Enabled |
