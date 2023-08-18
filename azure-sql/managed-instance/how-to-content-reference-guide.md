---
title: Configure & manage content reference
titleSuffix: Azure SQL Managed Instance
description: A reference guide of content that teaches you how to configure and manage Azure SQL Managed Instance.
author: MashaMSFT
ms.author: mathoma
ms.reviewer: mathoma, danil
ms.date: 03/22/2022
ms.service: sql-managed-instance
ms.subservice: deployment-configuration
ms.topic: conceptual
ms.custom:
  - sqldbrb=1
  - ignite-fall-2021
---
# Azure SQL Managed Instance content reference
[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

In this article you can find a content reference to various guides, scripts, and explanations that help you manage and configure Azure SQL Managed Instance.

## Load data

- [SQL Server to Azure SQL Managed Instance Guide](../migration-guides/managed-instance/sql-server-to-managed-instance-guide.md): Learn about the recommended migration process and tools for migration to Azure SQL Managed Instance.
- [Migrate TDE cert to Azure SQL Managed Instance](tde-certificate-migrate.md): If your SQL Server database is protected with transparent data encryption (TDE), you would need to migrate the certificate that SQL Managed Instance can use to decrypt the backup that you want to restore in Azure.
- [Import a DB from a BACPAC](../database/database-import.md)
- [Export a DB to BACPAC](../database/database-export.md)
- [Load data with BCP](../load-from-csv-with-bcp.md)
- [Load data with Azure Data Factory](/azure/data-factory/connector-azure-sql-database?toc=/azure/sql-database/toc.json)

## Network configuration

- [Determine subnet size](vnet-subnet-determine-size.md):
  Since the subnet cannot be resized after SQL Managed Instance is deployed, you need to calculate what IP range of addresses is required for the number and types of managed instances you plan to deploy to the subnet. 
- [Create a new VNet and subnet](virtual-network-subnet-create-arm-template.md):
  Configure the virtual network and subnet according to the [network requirements](connectivity-architecture-overview.md#network-requirements). 
- [Configure an existing VNet and subnet](vnet-existing-add-subnet.md):
  Verify network requirements and configure your existing virtual network and subnet to deploy SQL Managed Instance.
- [Configure service endpoint policies for Azure Storage (Preview)](service-endpoint-policies-configure.md):
  Secure your subnet against erroneous or malicious data exfiltration into unauthorized Azure Storage accounts.
- [Resolving private DNS names in Azure SQL Managed Instance](resolve-private-domain-names.md):
  Configure custom DNS servers to establish access from SQL Managed Instance to an external resource, such as scenarios involving linked servers or database mail.
- [Find the management endpoint IP address](management-endpoint-find-ip-address.md): 
  Determine the public endpoint that SQL Managed Instance is using for management purposes. 
- [Verify built-in firewall protection](management-endpoint-verify-built-in-firewall.md):
  Verify that SQL Managed Instance allows traffic only on necessary ports, and other built-in firewall rules. 
- [Connect applications](connect-application-instance.md): 
  Learn about different patterns for connecting the applications to SQL Managed Instance.

## Feature configuration

- [Configure Azure AD auth](../database/authentication-aad-configure.md)
- [Configure conditional access](../database/conditional-access-configure.md)
- [Azure AD Multi-Factor Authentication](../database/authentication-mfa-ssms-overview.md)
- [Configure auto-failover group](auto-failover-group-configure-sql-mi.md) to automatically failover all databases on an instance to a secondary instance in another region in the event of a disaster. 
- [Configure a temporal retention policy](../database/temporal-tables-retention-policy.md)
- [Configure In-Memory OLTP](../in-memory-oltp-configure.md)
- [Configure Azure Automation](../database/automation-manage.md)
- [Transactional replication](replication-between-two-instances-configure-tutorial.md) enables you to replicate your data between managed instances, or from SQL Server on-premises to SQL Managed Instance, and vice versa.
- [Configure threat detection](threat-detection-configure.md) – [threat detection](../database/threat-detection-overview.md) is a built-in Azure SQL Managed Instance feature that detects various potential attacks such as SQL injection or access from suspicious locations. 
- [Creating alerts](alerts-create.md) enables you to set up alerts on monitored metrics such as CPU utilization, storage space consumption, IOPS and others for SQL Managed Instance. 

### Transparent Data Encryption

- [Configure TDE with BYOK](../database/transparent-data-encryption-byok-configure.md)
- [Rotate TDE BYOK keys](../database/transparent-data-encryption-byok-key-rotation.md)
- [Remove a TDE protector](../database/transparent-data-encryption-byok-remove-tde-protector.md)

### Managed Instance link feature

- [Prepare environment for link feature](managed-instance-link-preparation.md)
- [Replicate database with link feature in SSMS](managed-instance-link-use-ssms-to-replicate-database.md)
- [Replicate database with Azure SQL Managed Instance link feature with T-SQL and PowerShell scripts](managed-instance-link-use-scripts-to-replicate-database.md)
- [Failover database with link feature in SSMS - Azure SQL Managed Instance](managed-instance-link-use-ssms-to-failover-database.md)
- [Failover (migrate) database with Azure SQL Managed Instance link feature with T-SQL and PowerShell scripts](managed-instance-link-use-scripts-to-failover-database.md)
- [Best practices with link feature for Azure SQL Managed Instance](managed-instance-link-best-practices.md)


## Monitoring and tuning

- [Manual tuning](../database/performance-guidance.md)
- [Use DMVs to monitor performance](monitoring-with-dmvs.md)
- [Use Query Store to monitor performance](/sql/relational-databases/performance/best-practice-with-the-query-store#Insight)
- [Troubleshoot performance with Intelligent Insights](../database/intelligent-insights-troubleshoot-performance.md)
- [Use the Intelligent Insights diagnostics log](../database/intelligent-insights-use-diagnostics-log.md)
- [Monitor In-Memory OLTP space](../in-memory-oltp-monitor-space.md)

### Extended events

- [Extended events](../database/xevent-db-diff-from-svr.md)
- [Store extended events into an event file](../database/xevent-code-event-file.md)
- [Store extended events into a ring buffer](../database/xevent-code-ring-buffer.md)

### Alerting

- [Create alerts on managed instance](alerts-create.md)

## Operations

- [User-initiated manual failover on SQL Managed Instance](user-initiated-failover.md)

## Develop applications

- [Connectivity](../database/connect-query-content-reference-guide.md#libraries)
- [Use Spark Connector](/azure/cosmos-db/create-sql-api-spark)
- [Authenticate an app](../database/application-authentication-get-client-id-keys.md)
- [Use batching for better performance](../performance-improve-use-batching.md)
- [Connectivity guidance](../database/troubleshoot-common-connectivity-issues.md)
- [DNS aliases](../database/dns-alias-overview.md)
- [Set up a DNS alias by using PowerShell](../database/dns-alias-powershell-create.md)
- [Ports - ADO.NET](../database/adonet-v12-develop-direct-route-ports.md)
- [C and C ++](../database/develop-cplusplus-simple.md)
- [Excel](../database/connect-excel.md)

## Design applications

- [Design for disaster recovery](../database/designing-cloud-solutions-for-disaster-recovery.md)
- [Design for elastic pools](../database/disaster-recovery-strategies-for-applications-with-elastic-pool.md)
- [Design for app upgrades](../database/manage-application-rolling-upgrade.md)

### Design Multi-tenant SaaS applications

- [SaaS design patterns](../database/saas-tenancy-app-design-patterns.md)
- [SaaS video indexer](../database/saas-tenancy-video-index-wingtip-brk3120-20171011.md)
- [SaaS app security](../database/saas-tenancy-elastic-tools-multi-tenant-row-level-security.md)

## Next steps

Get started by [deploying SQL Managed Instance](instance-create-quickstart.md).
