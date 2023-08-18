---
title: "SQL Server to SQL Managed Instance: Migration overview"
description: Learn about the tools and options available to migrate your SQL Server databases to Azure SQL Managed Instance.
author: croblesm
ms.author: roblescarlos
ms.reviewer: mathoma, danil, randolphwest
ms.date: 01/06/2023
ms.service: sql-managed-instance
ms.subservice: migration-guide
ms.custom: build-2023, build-2023-dataai
ms.topic: how-to
---
# Migration overview: SQL Server to Azure SQL Managed Instance

[!INCLUDE[appliesto--sqlmi](../../includes/appliesto-sqlmi.md)]

Learn about the options and considerations for migrating your SQL Server databases to Azure SQL Managed Instance. 

You can migrate SQL Server databases running on-premises or on: 

- SQL Server on Virtual Machines
- Amazon EC2 (Elastic Compute Cloud)
- Amazon RDS (Relational Database Service) for SQL Server
- Google Compute Engine
- Cloud SQL for SQL Server - GCP (Google Cloud Platform)

For other migration guides, see [Database Migration](/data-migration). 

## Overview

[Azure SQL Managed Instance](../../managed-instance/sql-managed-instance-paas-overview.md) is a recommended target option for SQL Server workloads that require a fully managed service without having to manage virtual machines or their operating systems. SQL Managed Instance enables you to move your on-premises applications to Azure with minimal application or database changes. It offers complete isolation of your instances with native virtual network support. 

Be sure to review the SQL Server database engine features [available in Azure SQL Managed Instance](../../database/features-comparison.md) to validate the supportability of your migration target.  

## Considerations 

The key factors to consider when you're evaluating migration options are: 
- Number of servers and databases
- Size of databases
- Acceptable business downtime during the migration process 

One of the key benefits of migrating your SQL Server databases to SQL Managed Instance is that you can choose to migrate the entire instance or just a subset of individual databases. Carefully plan to include the following in your migration process: 
- All databases that need to be colocated to the same instance 
- Instance-level objects required for your application, including logins, credentials, SQL Agent jobs and operators, and server-level triggers 

> [!NOTE]
>  
> Azure SQL Managed Instance guarantees 99.99 percent availability, even in critical scenarios. Overhead caused by some features in SQL Managed Instance can't be disabled. For more information, see the [Key causes of performance differences between SQL Managed Instance and SQL Server](https://azure.microsoft.com/blog/key-causes-of-performance-differences-between-sql-managed-instance-and-sql-server/) blog entry.

## Choose an appropriate target

You can use the [Azure SQL migration extension for Azure Data Studio](/sql/azure-data-studio/extensions/azure-sql-migration-extension) to get right-sized Azure SQL Managed Instance recommendation. The extension collects performance data from your source SQL Server instance to provide right-sized Azure recommendation that meets your workload's performance needs with minimal cost. To learn more, see [Get right-sized Azure recommendation for your on-premises SQL Server database(s)](/azure/dms/ads-sku-recommend)

The following general guidelines can help you choose the right service tier and characteristics of SQL Managed Instance to help match your [performance baseline](sql-server-to-managed-instance-performance-baseline.md): 

- Use the CPU usage baseline to provision a managed instance that matches the number of cores that your instance of SQL Server uses. It might be necessary to scale resources to match the [hardware configuration characteristics](../../managed-instance/resource-limits.md#hardware-configuration-characteristics). 
- Use the memory usage baseline to choose a [vCore option](../../managed-instance/resource-limits.md#service-tier-characteristics) that appropriately matches your memory allocation. 
- Use the baseline I/O latency of the file subsystem to choose between the General Purpose (latency greater than 5 ms) and Business Critical (latency less than 3 ms) service tiers. 
- Use the baseline throughput to preallocate the size of the data and log files to achieve expected I/O performance. 

You can choose compute and storage resources during deployment and then [change them afterward by using the Azure portal](../../database/scale-resources.md), without incurring downtime for your application. 

> [!IMPORTANT]
>  
> Any discrepancy in the [virtual network requirements for managed instances](../../managed-instance/connectivity-architecture-overview.md#network-requirements) can prevent you from creating new instances or using existing ones. Learn more about [creating new](../../managed-instance/virtual-network-subnet-create-arm-template.md) and [configuring existing](../../managed-instance/vnet-existing-add-subnet.md) networks. 

Another key consideration in the selection of the target service tier in Azure SQL Managed Instance (General Purpose versus Business Critical) is the availability of certain features, like In-Memory OLTP, that are available only in the Business Critical tier. 

### SQL Server VM alternative

Your business might have requirements that make [SQL Server on Azure Virtual Machines](../../virtual-machines/windows/sql-server-on-azure-vm-iaas-what-is-overview.md) a more suitable target than Azure SQL Managed Instance. 

If one of the following conditions applies to your business, consider moving to a SQL Server virtual machine (VM) instead: 

- You require direct access to the operating system or file system, such as to install third-party or custom agents on the same virtual machine with SQL Server. 
- You have strict dependency on features that are still not supported, such as FileStream/FileTable, PolyBase, and cross-instance transactions. 
- You need to stay at a specific version of SQL Server (2012, for example). 
- Your compute requirements are much lower than a managed instance offers (one vCore, for example), and database consolidation is not an acceptable option. 

## Migration tools

We recommend the following migration tools: 

|Technology | Description|
|---------|---------|
|[Azure SQL Migration extension for Azure Data Studio](/azure/dms/migration-using-azure-data-studio)| Powered by the [Azure Database Migration service](/azure/dms/dms-overview), the Azure SQL Migration extension for Azure Data Studio helps you to assess your database requirements to understand your migration readiness, get the right-sized SKU recommendations for Azure resources, and migrate your SQL Server database to Azure. You can migrate single databases or at scale using [PowerShell and Azure CLI](/azure/dms/migration-dms-powershell-cli). |
| [Azure Migrate](/azure/migrate/how-to-create-azure-sql-assessment) | This Azure service helps you discover and assess your SQL data estate at scale on VMware. It provides Azure SQL deployment recommendations, target sizing, and monthly estimates. | 
|[Native backup and restore](../../managed-instance/restore-sample-database-quickstart.md) | SQL Managed Instance supports restore of native SQL Server database backups (.bak files). It's the easiest migration option for customers who can provide full database backups to Azure Storage.| 
|[Log Replay Service](../../managed-instance/log-replay-service-migrate.md) | This cloud service is enabled for SQL Managed Instance based on SQL Server log-shipping technology. It's a migration option for customers who can provide full, differential, and log database backups to Azure Storage. Log Replay Service is used to restore backup files from Azure Blob Storage to SQL Managed Instance.| 
|[Managed Instance link](../../managed-instance/managed-instance-link-feature-overview.md) | This feature enables online migration to SQL Managed Instance using Always On technology. It's a migration option for customers who require database on SQL Managed Instance to be accessible in R/O mode while migration is in progress, who need to keep the migration running for prolonged periods of time (weeks or months at the time), who require true online replication to Business Critical service tier, and for customers who require the most performant minimum downtime migration. | 

The following table lists alternative migration tools: 

|**Technology** |**Description**  |
|---------|---------|
|[Transactional replication](../../managed-instance/replication-transactional-overview.md) | Replicate data from source SQL Server database tables to SQL Managed Instance by providing a publisher-subscriber type migration option while maintaining transactional consistency. | 
|[Bulk copy](/sql/relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server)| The [bulk copy program (bcp) tool](/sql/tools/bcp-utility) copies data from an instance of SQL Server into a data file. Use the tool to export the data from your source and import the data file into the target SQL managed instance.<br/><br/>For high-speed bulk copy operations to move data to Azure SQL Managed Instance, you can use the [Smart Bulk Copy tool](/samples/azure-samples/smartbulkcopy/smart-bulk-copy/) to maximize transfer speed by taking advantage of parallel copy tasks. | 
|[Import Export Wizard/BACPAC](../../database/database-import.md?tabs=azure-powershell)| [BACPAC](/sql/relational-databases/data-tier-applications/data-tier-applications#bacpac) is a Windows file with a .bacpac extension that encapsulates a database's schema and data. You can use BACPAC to both export data from a SQL Server source and import the data back into Azure SQL Managed Instance. |  
|[Azure Data Factory](/azure/data-factory/connector-azure-sql-managed-instance)| The [Copy activity](/azure/data-factory/copy-activity-overview) in Azure Data Factory migrates data from source SQL Server databases to SQL Managed Instance by using built-in connectors and an [integration runtime](/azure/data-factory/concepts-integration-runtime).<br/><br/>Data Factory supports a wide range of [connectors](/azure/data-factory/connector-overview) to move data from SQL Server sources to SQL Managed Instance. |

## Compare migration options

Compare migration options to choose the path that's appropriate to your business needs. 

The following table compares the recommended migration options: 

|Migration option  |When to use  |Considerations  |
|---------|---------|---------|
| [Azure SQL Migration extension for Azure Data Studio](/azure/dms/migration-using-azure-data-studio) | - Migrate single databases or at scale. </br> - Can run in both online and offline modes. </br> </br> Supported sources: </br> - SQL Server (2005 onwards) on-premises, or on Azure Virtual Machines </br> - SQL Server on Amazon EC2 </br> - Amazon RDS for SQL Server </br> - SQL Server on Google Compute Engine | - Migrations at scale can be automated via [PowerShell or Azure CLI](/azure/dms/migration-dms-powershell-cli). </br> </br> - Time to complete migration depends on database size and the number of objects in the database. </br> </br> - Azure Data Studio is required when you are not using PowerShell or Azure CLI. |
|[Native backup and restore](../../managed-instance/restore-sample-database-quickstart.md) | - Migrate individual line-of-business application databases.<br/>- Quick and easy migration without a separate migration service or tool.<br/><br/>Supported sources:<br/>- SQL Server (2005 to 2019) on-premises or Azure VM<br/>- Amazon EC2<br/>- GCP Compute SQL Server VM | - Database backup uses multiple threads to optimize data transfer to Azure Blob Storage, but partner bandwidth and database size can affect transfer rate.<br/>- Downtime should accommodate the time required to perform a full backup and restore (which is a size of data operation).| 
|[Log Replay Service](../../managed-instance/log-replay-service-migrate.md) | - Migrate individual line-of-business application databases.<br/>- More control is needed for database migrations.<br/><br/>Supported sources:<br/>- SQL Server (2008 to 2019) on-premises or Azure VM<br/>- Amazon EC2  </br> - Amazon RDS for SQL Server <br/> - GCP Compute SQL Server VM | - The migration entails making full database backups on SQL Server and copying backup files to Azure Blob Storage. Log Replay Service is used to restore backup files from Azure Blob Storage to SQL Managed Instance.<br/>- Databases being restored during the migration process will be in a restoring mode and can't be used for read or write workloads until the process is complete.| 
|[Link feature for Azure SQL Managed Instance](../../managed-instance/managed-instance-link-feature-overview.md) | - Migrate individual line-of-business application databases.<br/>- More control is needed for database migrations.<br/>- Minimum downtime migration is needed.<br/><br/>Supported sources:<br/>- SQL Server (2016 to 2019) on-premises or Azure VM<br/>- Amazon EC2<br/>- GCP Compute SQL Server VM | - The migration entails establishing a network connection between SQL Server and SQL Managed Instance, and opening communication ports.<br/>- Uses [Always On availability group](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server) technology to replicate database near real-time, making an exact replica of the SQL Server database on SQL Managed Instance.<br/>- The database can be used for read-only access on SQL Managed Instance while migration is in progress.<br/>- Provides the best performance during migration with minimum downtime. | 

The following table compares the alternative migration options: 

|Method or technology |When to use |Considerations  |
|---------|---------|---------|
|[Transactional replication](../../managed-instance/replication-transactional-overview.md) | - Migrate by continuously publishing changes from source database tables to target SQL Managed Instance database tables.<br/>- Do full or partial database migrations of selected tables (subset of a database).<br/><br/>Supported sources:<br/>- SQL Server (2012 to 2019) with some limitations<br/>- Amazon EC2<br/>- GCP Compute SQL Server VM |<br/>- Setup is relatively complex compared to other migration options.<br/>- Provides a continuous replication option to migrate data (without taking the databases offline).<br/>- Transactional replication has limitations to consider when you're setting up the publisher on the source SQL Server instance. See [Limitations on publishing objects](/sql/relational-databases/replication/publish/publish-data-and-database-objects#limitations-on-publishing-objects) to learn more.<br/>- Capability to [monitor replication activity](/sql/relational-databases/replication/monitor/monitoring-replication) is available.    |
|[Bulk copy](/sql/relational-databases/import-export/import-and-export-bulk-data-by-using-the-bcp-utility-sql-server)| - Do full or partial data migrations.<br/>- Can accommodate downtime.<br/><br/>Supported sources:<br/>- SQL Server (2005 to 2019) on-premises or Azure VM<br/>- Amazon EC2 <br/> - Amazon RDS for SQL Server<br/>- GCP Compute SQL Server VM   | - Requires downtime for exporting data from the source and importing into the target.<br/>- The file formats and data types used in the export or import need to be consistent with table schemas. |
|[Import Export Wizard/BACPAC](../../database/database-import.md)| - Migrate individual line-of-business application databases.<br/>- Suited for smaller databases.<br/>Doesn't require a separate migration service or tool.<br/><br/>Supported sources:<br/>- SQL Server (2005 to 2019) on-premises or Azure VM<br/>- Amazon EC2<br/>- Amazon RDS<br/>- GCP Compute SQL Server VM  |<br/>- Requires downtime because data needs to be exported at the source and imported at the destination.<br/>- The file formats and data types used in the export or import need to be consistent with table schemas to avoid truncation or data-type mismatch errors.<br/>- Time taken to export a database with a large number of objects can be significantly higher. |
|[Azure Data Factory](/azure/data-factory/connector-azure-sql-managed-instance)| - Migrate and/or transform data from source SQL Server databases.<br/>- Merging data from multiple sources of data to Azure SQL Managed Instance is typically for business intelligence (BI) workloads.<br/>- Requires creating data movement pipelines in Data Factory to move data from source to destination.<br/>- [Cost](https://azure.microsoft.com/pricing/details/data-factory/data-pipeline/) is an important consideration and is based on factors like pipeline triggers, activity runs, and duration of data movement. |

## Feature interoperability 

There are more considerations when you're migrating workloads that rely on other SQL Server features. 

### SQL Server Integration Services

Migrate SQL Server Integration Services (SSIS) packages and projects in SSISDB to Azure SQL Managed Instance by using [Azure Database Migration Service](/azure/dms/how-to-migrate-ssis-packages-managed-instance). 

Only SSIS packages in SSISDB starting with SQL Server 2012 are supported for migration. Convert older SSIS packages before migration. See the [project conversion tutorial](/sql/integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model) to learn more. 

### SQL Server Reporting Services

You can migrate SQL Server Reporting Services (SSRS) reports to paginated reports in Power BI. Use the [RDL Migration Tool](https://github.com/microsoft/RdlMigration) to help prepare and migrate your reports. Microsoft developed this tool to help customers migrate Report Definition Language (RDL) reports from their SSRS servers to Power BI. It's available on GitHub, and it documents an end-to-end walkthrough of the migration scenario. 

### SQL Server Analysis Services

SQL Server Analysis Services tabular models from SQL Server 2012 and later can be migrated to Azure Analysis Services, which is a platform as a service (PaaS) deployment model for the Analysis Services tabular model in Azure. You can learn more about migrating on-premises models to Azure Analysis Services in [this video tutorial](https://azure.microsoft.com/resources/videos/azure-analysis-services-moving-models/).

Alternatively, you can consider migrating your on-premises Analysis Services tabular models to [Power BI Premium by using the new XMLA read/write endpoints](/power-bi/admin/service-premium-connect-tools). 

### High availability

The SQL Server high-availability features Always On failover cluster instances and Always On availability groups become obsolete on the target SQL managed instance. High-availability architecture is already built into both [General Purpose (standard availability model)](../../database/high-availability-sla.md#locally-redundant-availability) and [Business Critical (premium availability model)](../../database/high-availability-sla.md#locally-redundant-availability) service tiers for SQL Managed Instance. The premium availability model also provides read scale-out that allows connecting into one of the secondary nodes for read-only purposes.     

Beyond the high-availability architecture that's included in SQL Managed Instance, the [auto-failover groups](../../managed-instance/auto-failover-group-sql-mi.md) feature allows you to manage the replication and failover of databases in a managed instance to another region. 

### SQL Agent jobs

Use the offline Azure Database Migration Service option to migrate [SQL Agent jobs](/azure/dms/howto-sql-server-to-azure-sql-managed-instance-powershell-offline). Otherwise, script the jobs in Transact-SQL (T-SQL) by using SQL Server Management Studio and then manually re-create them on the target SQL managed instance. 

> [!IMPORTANT]
>  
> Currently, Azure Database Migration Service supports only jobs with T-SQL subsystem steps. Jobs with SSIS package steps have to be manually migrated. 

### Logins and groups

Move SQL logins from the SQL Server source to Azure SQL Managed Instance by using Database Migration Service in offline mode.  Use the [Select logins](/azure/dms/tutorial-sql-server-to-managed-instance#select-logins) pane in the Migration Wizard to migrate logins to your target SQL managed instance. 

By default, Azure Database Migration Service supports migrating only SQL logins. However, you can enable the migration of Windows logins by:

- Ensuring that the target SQL managed instance has Azure Active Directory (Azure AD) read access. A user who has the Global Administrator role can configure that access via the Azure portal.
- Configuring Azure Database Migration Service to enable Windows user or group login migrations. You set this up via the Azure portal, on the **Configuration** page. After you enable this setting, restart the service for the changes to take effect.

After you restart the service, Windows user or group logins appear in the list of logins available for migration. For any Windows user or group logins that you migrate, you're prompted to provide the associated domain name. Service user accounts (accounts with the domain name NT AUTHORITY) and virtual user accounts (accounts with the domain name NT SERVICE) aren't supported. To learn more, see [How to migrate Windows users and groups in a SQL Server instance to Azure SQL Managed Instance using T-SQL](../../managed-instance/migrate-sql-server-users-to-instance-transact-sql-tsql-tutorial.md).

Alternatively, you can use the [PowerShell utility](https://www.microsoft.com/download/details.aspx?id=103111) specially designed by Microsoft data migration architects. The utility uses PowerShell to create a T-SQL script to re-create logins and select database users from the source to the target. 

The PowerShell utility automatically maps Windows Server Active Directory accounts to Azure AD accounts, and it can do a UPN lookup for each login against the source Active Directory instance. The utility scripts custom server and database roles, along with role membership and user permissions. Contained databases aren't yet supported, and only a subset of possible SQL Server permissions is scripted. 

### Encryption

When you're migrating databases protected by [Transparent Data Encryption](../../database/transparent-data-encryption-tde-overview.md) to a managed instance by using the native restore option, [migrate the corresponding certificate](../../managed-instance/tde-certificate-migrate.md) from the source SQL Server instance to the target SQL managed instance *before* database restore. 

### System databases

Restore of system databases isn't supported. To migrate instance-level objects (stored in the `master` and `msdb` databases), script them by using T-SQL and then re-create them on the target managed instance. 

### In-Memory OLTP (memory-optimized tables)

SQL Server provides an In-Memory OLTP capability. It allows usage of memory-optimized tables, memory-optimized table types, and natively compiled SQL modules to run workloads that have high-throughput and low-latency requirements for transactional processing. 

> [!IMPORTANT]
>  
> In-Memory OLTP is supported only in the Business Critical tier in Azure SQL Managed Instance. It's not supported in the General Purpose tier.

If you have memory-optimized tables or memory-optimized table types in your on-premises SQL Server instance and you want to migrate to Azure SQL Managed Instance, you should either:

- Choose the Business Critical tier for your target SQL managed instance that supports In-Memory OLTP.
- If you want to migrate to the General Purpose tier in Azure SQL Managed Instance, remove memory-optimized tables, memory-optimized table types, and natively compiled SQL modules that interact with memory-optimized objects before migrating your databases. You can use the following T-SQL query to identify all objects that need to be removed before migration to the General Purpose tier:

   ```sql
   SELECT * FROM sys.tables WHERE is_memory_optimized=1
   SELECT * FROM sys.table_types WHERE is_memory_optimized=1
   SELECT * FROM sys.sql_modules WHERE uses_native_compilation=1
   ```

To learn more about in-memory technologies, see [Optimize performance by using in-memory technologies in Azure SQL Database and Azure SQL Managed Instance](../../in-memory-oltp-overview.md).

## Advanced features 

Be sure to take advantage of the advanced cloud-based features in SQL Managed Instance. For example, you don't need to worry about managing backups because the service does it for you. You can restore to any [point in time within the retention period](../../database/recovery-using-backups.md#point-in-time-restore). Additionally, you don't need to worry about setting up high availability, because [high availability is built in](../../database/high-availability-sla.md). 

To strengthen security, consider using [Azure AD authentication](../../database/authentication-aad-overview.md), [auditing](../../managed-instance/auditing-configure.md), [threat detection](../../database/azure-defender-for-sql.md), [row-level security](/sql/relational-databases/security/row-level-security), and [dynamic data masking](/sql/relational-databases/security/dynamic-data-masking).

In addition to advanced management and security features, SQL Managed Instance provides advanced tools that can help you [monitor and tune your workload](../../database/monitor-tune-overview.md). [Azure SQL Analytics](/azure/azure-monitor/insights/azure-sql) allows you to monitor a large set of managed instances in a centralized way. [Automatic tuning](/sql/relational-databases/automatic-tuning/automatic-tuning#automatic-plan-correction) in managed instances continuously monitors performance of your SQL plan execution and automatically fixes the identified performance problems. 

Some features are available only after the [database compatibility level](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) is changed to the latest compatibility level (150). 

## Migration assets 

For more assistance, see the following resources that were developed for real-world migration projects.

|Asset  |Description  |
|---------|---------|
|[Data workload assessment model and tool](https://www.microsoft.com/download/details.aspx?id=103130)| This tool provides suggested "best fit" target platforms, cloud readiness, and an application/database remediation level for a workload. It offers simple, one-click calculation and report generation that helps to accelerate large estate assessments by providing an automated and uniform decision process for target platforms.|
|[Utility to move on-premises SQL Server logins to Azure SQL Managed Instance](https://www.microsoft.com/download/details.aspx?id=103111)|A PowerShell script can create a T-SQL command script to re-create logins and select database users from on-premises SQL Server to Azure SQL Managed Instance. The tool allows automatic mapping of Windows Server Active Directory accounts to Azure AD accounts, along with optionally migrating SQL Server native logins.|
|[Perfmon data collection automation by using Logman](https://www.microsoft.com/download/details.aspx?id=103114)|You can use the Logman tool to collect Perfmon data (to help you understand baseline performance) and get migration target recommendations. This tool uses logman.exe to create the command that will create, start, stop, and delete performance counters set on a remote SQL Server instance.|

The Data SQL Engineering team developed these resources. This team's core charter is to unblock and accelerate complex modernization for data platform migration projects to Microsoft's Azure data platform.

## Next steps

- To start migrating your SQL Server databases to Azure SQL Managed Instance, see the [SQL Server to Azure SQL Managed Instance migration guide](sql-server-to-managed-instance-guide.md).

- For a matrix of services and tools that can help you with database and data migration scenarios as well as specialty tasks, see [Services and tools for data migration](/azure/dms/dms-tools-matrix).

- To learn more about Azure SQL Managed Instance, see:
   - [Service tiers in Azure SQL Managed Instance](../../managed-instance/sql-managed-instance-paas-overview.md#service-tiers)
   - [Differences between SQL Server and Azure SQL Managed Instance](../../managed-instance/transact-sql-tsql-differences-sql-server.md)
   - [Azure Total Cost of Ownership Calculator](https://azure.microsoft.com/pricing/tco/calculator/) 

- To learn more about the framework and adoption cycle for cloud migrations, see:
   -  [Cloud Adoption Framework for Azure](/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-scale)
   -  [Best practices for costing and sizing workloads migrated to Azure](/azure/cloud-adoption-framework/migrate/azure-best-practices/migrate-best-practices-costs) 

- To assess the application access layer, see [Data Access Migration Toolkit (Preview)](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit).

- For details on how to perform A/B testing at the data access layer, see [Database Experimentation Assistant](/sql/dea/database-experimentation-assistant-overview).
