---
title: "SQL Server to Azure SQL Managed Instance: Migration guide"
description: This guide teaches you to migrate your SQL Server databases to Azure SQL Managed Instance.
author: croblesm
ms.author: roblescarlos
ms.reviewer: mathoma, danil, randolphwest
ms.date: 01/06/2023
ms.service: sql-managed-instance
ms.subservice: migration-guide
ms.topic: how-to
---
# Migration guide: SQL Server to Azure SQL Managed Instance

[!INCLUDE[appliesto-sqldb-sqlmi](../../includes/appliesto-sqlmi.md)]

This guide helps you migrate your SQL Server instance to Azure SQL Managed Instance. 

You can migrate SQL Server running on-premises or on: 

- SQL Server on Virtual Machines
- Amazon EC2 (Elastic Compute Cloud)
- Amazon RDS (Relational Database Service) for SQL Server
- Google Compute Engine
- Cloud SQL for SQL Server - GCP (Google Cloud Platform)

For more migration information, see the [migration overview](sql-server-to-managed-instance-overview.md). For other migration guides, see [Database Migration](/data-migration). 

:::image type="content" source="media/sql-server-to-managed-instance-overview/migration-process-flow-small.png" alt-text="Migration process flow":::

## Prerequisites 

To migrate your SQL Server to Azure SQL Managed Instance, make sure you have: 

- Chosen a [migration method](sql-server-to-managed-instance-overview.md#compare-migration-options) and the corresponding tools for your method.
- Install the [Azure SQL migration extension for Azure Data Studio](/sql/azure-data-studio/extensions/azure-sql-migration-extension).
- Created a target [Azure SQL Managed Instance](../../managed-instance/instance-create-quickstart.md)
- Configured connectivity and proper permissions to access both source and target. 
- Reviewed the SQL Server database engine features [available in Azure SQL Managed Instance](../../database/features-comparison.md). 

## Pre-migration

After you've verified that your source environment is supported, start with the pre-migration stage. Discover all of the existing data sources, assess migration feasibility, and identify any blocking issues that might prevent your migration.  

### Discover

In the Discover phase, scan the network to identify all SQL Server instances and features used by your organization. 

Use [Azure Migrate](/azure/migrate/migrate-services-overview) to assess migration suitability of on-premises servers, perform performance-based sizing, and provide cost estimations for running them in Azure. 

Alternatively, use the [Microsoft Assessment and Planning Toolkit (the "MAP Toolkit")](https://www.microsoft.com/download/details.aspx?id=7826) to assess your current IT infrastructure. The toolkit provides a powerful inventory, assessment, and reporting tool to simplify the migration planning process. 

For more information about tools available to use for the Discover phase, see [Services and tools available for data migration scenarios](/azure/dms/dms-tools-matrix). 

After data sources have been discovered, assess any on-premises SQL Server instance(s) that can be migrated to Azure SQL Managed Instance to identify migration blockers or compatibility issues.
Proceed to the following steps to assess and migrate databases to Azure SQL Managed Instance:

:::image type="content" source="media/sql-server-to-managed-instance-overview/migration-process-sql-managed-instance-steps.png" alt-text="Steps for migration to Azure SQL Managed Instance":::

- [Assess SQL Managed Instance compatibility](#assess) where you should ensure that there are no blocking issues that can prevent your migrations.
  This step also includes creation of a [performance baseline](sql-server-to-managed-instance-performance-baseline.md#create-a-baseline) to determine resource usage on your source SQL Server instance. This step is needed if you want to deploy a properly sized managed instance and verify that performance after migration isn't affected.
- [Choose app connectivity options](../../managed-instance/connect-application-instance.md).
- [Deploy to an optimally sized managed instance](#deploy-to-an-optimally-sized-managed-instance) where you'll choose technical characteristics (number of vCores, amount of memory) and performance tier (Business Critical, General Purpose) of your managed instance.
- [Select migration method and migrate](sql-server-to-managed-instance-overview.md#compare-migration-options) where you migrate your databases using offline migration or online migration options.
- [Monitor and remediate applications](#monitor-and-remediate-applications) to ensure that you have expected performance.

### Assess 

[!INCLUDE [assess-estate-with-azure-migrate](../../includes/azure-migrate-to-assess-sql-data-estate.md)]

Determine whether SQL Managed Instance is compatible with the database requirements of your application. SQL Managed Instance is designed to provide easy lift and shift migration for most existing applications that use SQL Server. However, you may sometimes require features or capabilities that aren't yet supported and the cost of implementing a workaround is too high.

The [Azure SQL migration extension for Azure Data Studio](/azure/dms/migration-using-azure-data-studio) provides a seamless wizard based experience to assess, get Azure recommendations and migrate your SQL Server databases on-premises to SQL Server on Azure Virtual Machines. Besides, highlighting any migration blockers or warnings, the extension also includes an option for Azure recommendations to collect your databases' performance data [to recommend a right-sized Azure SQL Managed Instance](/azure/dms/ads-sku-recommend) to meet the performance needs of your workload (with the least price).

You can use the Azure SQL Migration extension for Azure Data Studio to assess databases to get:

- [Migration readiness - Assessment rules](./sql-server-to-sql-managed-instance-assessment-rules.md)
- [Azure right-sized recommendations](/azure/dms/ads-sku-recommend)

To assess your environment using the Azure SQL Migration extension, follow these steps:

1. Open the [Azure SQL Migration extension for Azure Data Studio](/sql/azure-data-studio/extensions/azure-sql-migration-extension).
1. Connect to your source SQL Server instance
1. Click the *Migrate to Azure SQL* button, in the Azure SQL Migration wizard in Azure Data Studio
1. Select databases for assessment, then click on next
1. Select your Azure SQL target, in this case, Azure SQL Managed Instance
1. Click on *View/Select* to review the assessment report
1. Look for migration blocking and feature parity issues. The assessment report can also be exported to a file that can be shared with other teams or personnel in your organization.
1. Determine the database compatibility level that minimizes post-migration efforts.

To get an Azure recommendation using the Azure SQL Migration extension, follow these steps:

1. Open the [Azure SQL Migration extension for Azure Data Studio](/sql/azure-data-studio/extensions/azure-sql-migration-extension).
1. Connect to your source SQL Server instance
1. Click the *Migrate to Azure SQL* button, in the Azure SQL Migration wizard in Azure Data Studio
1. Select databases for assessment, then click on next
1. Select your Azure SQL target, in this case, Azure SQL Managed Instance
1. Navigate to the Azure recommendations sections, click on *Get Azure recommendation*
1. Select Collect performance data now. Select a folder on your local computer to store the performance logs, and then select Start.
1. After 10 minutes, Azure Data Studio indicates that a recommendation is available for Azure SQL Managed Instance.
1. Check the Azure SQL Managed Instance card, in the Azure SQL target panel to review your Azure SQL Managed Instance SKU recommendation

To learn more, see [Tutorial: Migrate SQL Server to Azure SQL Managed Instance online by using Azure Data Studio](/azure/dms/tutorial-sql-server-managed-instance-online-ads).

To learn more, see [Tutorial: Migrate SQL Server to Azure SQL Managed Instance offline by using Azure Data Studio](/azure/dms/tutorial-sql-server-managed-instance-offline-ads).

If the assessment encounters multiple blockers to confirm that your database is not ready for an Azure SQL Managed Instance, then alternatively consider:

- [SQL Server on Azure Virtual Machines](../virtual-machines/sql-server-to-sql-on-azure-vm-migration-overview.md) if both SQL Database and SQL Managed Instance fail to be suitable targets.

#### Scaled assessments and analysis

The [Azure SQL Migration extension for Azure Data Studio](/sql/azure-data-studio/extensions/azure-sql-migration-extension) and  [Azure Migrate](https://azure.microsoft.com/services/azure-migrate) supports performing scaled assessments and consolidation of the assessment reports for analysis.

If you have multiple servers and databases that need to be assessed and analyzed at scale to provide a wider view of the data estate, see the following links to learn more:

- [Migrate databases at scale using automation (Preview) - Azure SQL Migration extension](/azure/dms/migration-dms-powershell-cli)
- [Performing scaled assessments using PowerShell - Azure Migrate](/sql/dma/dma-consolidatereports)
- [Analyzing assessment reports using Power BI - Azure Migrate](/sql/dma/dma-consolidatereports#dma-reports)

> [!IMPORTANT]
>  
>Running assessments at scale for multiple databases can also be automated using [DMA's Command Line Utility](/sql/dma/dma-commandline) which also allows the results to be uploaded to [Azure Migrate](/sql/dma/dma-assess-sql-data-estate-to-sqldb#view-target-readiness-assessment-results) for further analysis and target readiness.

### Deploy to an optimally sized managed instance

You can use the [Azure SQL migration extension for Azure Data Studio](/sql/azure-data-studio/extensions/azure-sql-migration-extension) to get right-sized Azure SQL Managed Instance recommendation. The extension collects performance data from your source SQL Server instance to provide right-sized Azure recommendation that meets your workload's performance needs with minimal cost. To learn more, see [Get right-sized Azure recommendation for your on-premises SQL Server database(s)](/azure/dms/ads-sku-recommend)

Based on the information in the discover and assess phase, create an appropriately sized target SQL Managed Instance. You can do so by using the [Azure portal](../../managed-instance/instance-create-quickstart.md), [PowerShell](../../managed-instance/scripts/create-configure-managed-instance-powershell.md), or an [Azure Resource Manager (ARM) Template](../../managed-instance/create-template-quickstart.md).

SQL Managed Instance is tailored for on-premises workloads that are planning to move to the cloud. It introduces a [purchasing model](../../database/service-tiers-vcore.md) that provides greater flexibility in selecting the right level of resources for your workloads. In the on-premises world, you're probably accustomed to sizing these workloads by using physical cores and IO bandwidth. The purchasing model for managed instance is based upon virtual cores, or "vCores," with additional storage and IO available separately. The vCore model is a simpler way to understand your compute requirements in the cloud versus what you use on-premises today. This purchasing model enables you to right-size your destination environment in the cloud. Some general guidelines that might help you to choose the right service tier and characteristics are described here:

- Based on the baseline CPU usage, you can provision a managed instance that matches the number of cores that you're using on SQL Server, having in mind that CPU characteristics might need to be scaled to match [VM characteristics where the managed instance is installed](../../managed-instance/resource-limits.md#hardware-configuration-characteristics).
- Based on the baseline memory usage, choose [the service tier that has matching memory](../../managed-instance/resource-limits.md#hardware-configuration-characteristics). The amount of memory can't be directly chosen, so you would need to select the managed instance with the amount of vCores that has matching memory (for example, 5.1 GB/vCore in standard-series (Gen5)).
- Based on the baseline IO latency of the file subsystem, choose between the General Purpose (latency greater than 5 ms) and Business Critical (latency less than 3 ms) service tiers.
- Based on baseline throughput, pre-allocate the size of data or log files to get expected IO performance.

You can choose compute and storage resources at deployment time and then change it afterward without introducing downtime for your application using the [Azure portal](../../database/scale-resources.md):

:::image type="content" source="media/sql-server-to-managed-instance-overview/managed-instance-sizing.png" alt-text="Managed Instance Sizing":::

To learn how to create the VNet infrastructure and a managed instance, see [Create a managed instance](../../managed-instance/instance-create-quickstart.md).

> [!IMPORTANT]
>  
> It is important to keep your destination VNet and subnet in accordance with [managed instance VNet requirements](../../managed-instance/connectivity-architecture-overview.md#network-requirements). Any incompatibility can prevent you from creating new instances or using those that you already created. Learn more about [creating new](../../managed-instance/virtual-network-subnet-create-arm-template.md) and [configuring existing](../../managed-instance/vnet-existing-add-subnet.md) networks.

## Migrate

After you have completed tasks associated with the Pre-migration stage, you're ready to perform the schema and data migration. 

Migrate your data using your chosen [migration method](sql-server-to-managed-instance-overview.md#compare-migration-options).

SQL Managed Instance targets user scenarios requiring mass database migration from on-premises or Azure VM database implementations. They are the optimal choice when you need to lift and shift the back end of the applications that regularly use instance level and/or cross-database functionalities. If this is your scenario, you can move an entire instance to a corresponding environment in Azure without the need to rearchitect your applications.

To move SQL instances, you need to plan carefully:

- The migration of all databases that need to be collocated (ones running on the same instance).
- The migration of instance-level objects that your application depends on, including logins, credentials, SQL Agent jobs and operators, and server-level triggers.

SQL Managed Instance is a managed service that allows you to delegate some of the regular DBA activities to the platform as they're built in. Therefore, some instance-level data doesn't need to be migrated, such as maintenance jobs for regular backups or Always On configuration, as [high availability](../../database/high-availability-sla.md) is built in.

This article covers two of the recommended migration options: 

- Azure SQL migration extension for Azure Data Studio - migration with near-zero downtime.
- Native `RESTORE DATABASE FROM URL` - uses native backups from SQL Server and requires some downtime.

This guide describes the two most popular options - Azure Database Migration Service (DMS) and native backup and restore.

For other migration tools, see [Compare migration options](sql-server-to-managed-instance-overview.md#compare-migration-options). 

### Migrate using the Azure SQL migration extension for Azure Data Studio (minimal downtime)

To perform a minimal downtime migration using Azure Data Studio, follow the high-level steps below. For a detailed step-by-step tutorial, see [Migrate SQL Server to an Azure SQL Managed Instance online using Azure Data Studio](/azure/dms/tutorial-sql-server-managed-instance-online-ads):

1. Download and install [Azure Data Studio](/sql/azure-data-studio/download-azure-data-studio) and the [Azure SQL migration extension](/sql/azure-data-studio/extensions/azure-sql-migration-extension).
1. Launch the Migrate to Azure SQL Migration wizard in the extension in Azure Data Studio.
1. Select databases for assessment and view migration readiness or issues (if any). Additionally, collect performance data and get right-sized Azure recommendation.
1. Select your Azure account and your target Azure SQL Managed Instance from your subscription.
1. Select the location of your database backups. Your database backups can either be located on an on-premises network share or in Azure Blob Storage container.
1. Create a new Azure Database Migration Service using the wizard in Azure Data Studio. If you've previously created an Azure Database Migration Service using Azure Data Studio, you can reuse the same if desired.
1. *Optional*: If your backups are on an on-premises network share, download and install [self-hosted integration runtime](https://www.microsoft.com/download/details.aspx?id=39717) on a machine that can connect to the source SQL Server, and the location containing the backup files.
1. Start the database migration and monitor the progress in Azure Data Studio. You can also monitor the progress under the Azure Database Migration Service resource in Azure portal.
1. Complete the cutover.
   1. Stop all incoming transactions to the source database.
   1. Make application configuration changes to point to the target database in Azure SQL Managed Instance.
   1. Take any tail log backups for the source database in the backup location specified.
   1. Ensure all database backups have the status Restored in the monitoring details page.
   1. Select Complete cutover in the monitoring details page.
   

### Backup and restore

One of the key capabilities of Azure SQL Managed Instance to enable quick and easy database migration is the native restore of database backup (`.bak`) files stored on [Azure Storage](https://azure.microsoft.com/services/storage/). Backing up and restoring are asynchronous operations based on the size of your database. 

The following diagram provides a high-level overview of the process:

:::image type="content" source="./media/sql-server-to-managed-instance-overview/migration-restore.png" alt-text="Diagram shows SQL Server with an arrow labeled BACKUP / Upload to URL flowing to Azure Storage and a second arrow labeled RESTORE from URL flowing from Azure Storage to a SQL Managed Instance.":::

> [!NOTE]
>  
> The time to take the backup,  upload it to Azure storage, and perform a native restore operation to Azure SQL Managed Instance is based on the size of the database. Factor a sufficient downtime to accommodate the operation for large databases. 

The following table provides more information regarding the methods you can use depending on 
source SQL Server version you're running:

|Step|SQL Engine and version|Backup/restore method|
|---|---|---|
|Put backup to Azure Storage|Prior to 2012 SP1 CU2|Upload .bak file directly to Azure Storage|
| |2012 SP1 CU2 - 2016|Direct backup using deprecated [WITH CREDENTIAL](/sql/t-sql/statements/restore-statements-transact-sql) syntax|
| |2016 and above|Direct backup using [WITH SAS CREDENTIAL](/sql/relational-databases/backup-restore/sql-server-backup-to-url)|
|Restore from Azure Storage to a managed instance| |[RESTORE FROM URL with SAS CREDENTIAL](../../managed-instance/restore-sample-database-quickstart.md)|

> [!IMPORTANT]
>
> - When you're migrating a database protected by [Transparent Data Encryption](../../database/transparent-data-encryption-tde-overview.md) to a managed instance using native restore option, the corresponding certificate from the on-premises or Azure VM SQL Server needs to be migrated before database restore. For detailed steps, see [Migrate a TDE cert to a managed instance](../../managed-instance/tde-certificate-migrate.md).
> - Restore of system databases is not supported. To migrate instance-level objects (stored in `master` or `msdb` databases), we recommend to script them out and run T-SQL scripts on the destination instance.

To migrate using backup and restore, follow these steps: 

1. Back up your database to Azure Blob Storage. For example, use [backup to url](/sql/relational-databases/backup-restore/sql-server-backup-to-url) in [SQL Server Management Studio](/sql/ssms/download-sql-server-management-studio-ssms). Use the [Microsoft Azure Tool](https://go.microsoft.com/fwlink/?LinkID=324399) to support databases earlier than SQL Server 2012 SP1 CU2. 
1. Connect to your Azure SQL Managed Instance using SQL Server Management Studio. 
1. Create a credential using a Shared Access Signature to access your Azure Blob storage account with your database backups. For example:

   ```sql
   CREATE CREDENTIAL [https://mitutorials.blob.core.windows.net/databases]
   WITH IDENTITY = 'SHARED ACCESS SIGNATURE'
   , SECRET = 'sv=2017-11-09&ss=bfqt&srt=sco&sp=rwdlacup&se=2028-09-06T02:52:55Z&st=2018-09-04T18:52:55Z&spr=https&sig=WOTiM%2FS4GVF%2FEEs9DGQR9Im0W%2BwndxW2CQ7%2B5fHd7Is%3D'
   ```
1. Restore the backup from the Azure storage blob container. For example: 

   ```sql
   RESTORE DATABASE [TargetDatabaseName] FROM URL =
     'https://mitutorials.blob.core.windows.net/databases/WideWorldImporters-Standard.bak'
   ```

1. Once restore completes, view the database in **Object Explorer** within SQL Server Management Studio. 

To learn more about this migration option, see [Restore a database to Azure SQL Managed Instance with SSMS](../../managed-instance/restore-sample-database-quickstart.md).

> [!NOTE]
>  
> A database restore operation is asynchronous and can be retried. You might get an error in SQL Server Management Studio if the connection breaks or a time-out expires. Azure SQL Database will keep trying to restore database in the background, and you can track the progress of the restore using the [sys.dm_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql) and [sys.dm_operation_status](/sql/relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database) views.

## Data sync and cutover

When using migration options that continuously replicate / sync data changes from source to the target, the source data and schema can change and drift from the target. During data sync, ensure that all changes on the source are captured and applied to the target during the migration process. 

After you verify that data is the same on both source and target, you can cut over from the source to the target environment. It's important to plan the cutover process with business / application teams to ensure minimal interruption during cutover doesn't affect business continuity. 

> [!IMPORTANT]
>  
> For details on the specific steps associated with performing a cutover as part of migrations using DMS, see [Performing migration cutover](/azure/dms/tutorial-sql-server-managed-instance-online#performing-migration-cutover).

## Post-migration

After you've successfully completed the migration stage, go through a series of post-migration tasks to ensure that everything is functioning smoothly and efficiently. 

The post-migration phase is crucial for reconciling any data accuracy issues and verifying completeness, and addressing performance issues with the workload. 

### Monitor and remediate applications 
Once you've completed the migration to a managed instance, you should track the application behavior and performance of your workload. This process includes the following activities:

- [Compare performance of the workload running on the managed instance](sql-server-to-managed-instance-performance-baseline.md#compare-performance) with the [performance baseline that you created on the source SQL Server instance](sql-server-to-managed-instance-performance-baseline.md#create-a-baseline).
- Continuously [monitor performance of your workload](sql-server-to-managed-instance-performance-baseline.md#monitor-performance) to identify potential issues and improvement.

### Perform tests

The test approach for database migration consists of the following activities:

1. **Develop validation tests**: To test database migration, you need to use SQL queries. You must create the validation queries to run against both the source and the target databases. Your validation queries should cover the scope you've defined.
1. **Set up test environment**: The test environment should contain a copy of the source database and the target database. Be sure to isolate the test environment.
1. **Run validation tests**: Run the validation tests against the source and the target, and then analyze the results.
1. **Run performance tests**: Run performance test against the source and the target, and then analyze and compare the results.

## Use advanced features 

You can take advantage of the advanced cloud-based features offered by SQL Managed Instance, such as [built-in high availability](../../database/high-availability-sla.md), [threat detection](../../database/azure-defender-for-sql.md), and [monitoring and tuning your workload](../../database/monitor-tune-overview.md). 

[Azure SQL Analytics](../../database/monitor-tune-overview.md) allows you to monitor a large set of managed instances in a centralized manner.

Some SQL Server features are only available once the [database compatibility level](/sql/relational-databases/databases/view-or-change-the-compatibility-level-of-a-database) is changed to the latest compatibility level (150). 

## Next steps

- See [Service and tools for data migration](/azure/dms/dms-tools-matrix) for a matrix of the Microsoft and third-party services and tools that are available to assist you with various database and data migration scenarios as well as specialty tasks.

- To learn more about the Azure SQL Migration extension see:

   - [Migrate databases with Azure SQL Migration extension for Azure Data Studio](/azure/dms/dms-overview#migrate-databases-with-azure-sql-migration-extension-for-azure-data-studio)

   - [Tutorial: Migrate SQL Server to Azure SQL Managed Instance online by using Azure Data Studio](/azure/dms/tutorial-sql-server-managed-instance-online-ads).

   - [Tutorial: Migrate SQL Server to Azure SQL Managed Instance offline by using Azure Data Studio](/azure/dms/tutorial-sql-server-managed-instance-offline-ads).


- To learn more about Azure SQL Managed Instance see:
   - [Service Tiers in Azure SQL Managed Instance](../../managed-instance/sql-managed-instance-paas-overview.md#service-tiers)
   - [Differences between SQL Server and Azure SQL Managed Instance](../../managed-instance/transact-sql-tsql-differences-sql-server.md)
   - [Azure total Cost of Ownership Calculator](https://azure.microsoft.com/pricing/tco/calculator/) 

- To learn more about the framework and adoption cycle for Cloud migrations, see
   -  [Cloud Adoption Framework for Azure](/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-scale)
   -  [Best practices for costing and sizing workloads migrate to Azure](/azure/cloud-adoption-framework/migrate/azure-best-practices/migrate-best-practices-costs) 

- To assess the Application access layer, see [Data Access Migration Toolkit (Preview)](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)

- For details on how to perform Data Access Layer A/B testing see [Database Experimentation Assistant](/sql/dea/database-experimentation-assistant-overview).