---
title: "Assessment rules for SQL Server to Azure SQL Database migration"
description: Assessment rules to identify issues with the source SQL Server instance that must be addressed before migrating to Azure SQL Database.
author: rajeshsetlem
ms.author: rsetlem
ms.reviewer: mathoma
ms.date: 12/15/2020
ms.service: sql-database
ms.subservice: migration-guide
ms.topic: how-to
ms.custom: ignite-fall-2021
---
# Assessment rules for SQL Server to Azure SQL Database migration
[!INCLUDE[appliesto--sqldb](../../includes/appliesto-sqldb.md)]

Migration tools validate your source SQL Server instance by running a number of assessment rules to identify issues that must be addressed before migrating your SQL Server database to Azure SQL Database. 

This article provides a list of the rules used to assess the feasibility of migrating your SQL Server database to Azure SQL Database. 

## Rules Summary

 | Rule Title | Level | Category | Details | 
 | - | - | - | - | 
 | AgentJobs | Instance | Warning | [SQL Server Agent jobs aren't available in Azure SQL Database.](#AgentJobs) | 
 | BulkInsert | Database | Issue | [BULK INSERT with non-Azure blob data source isn't supported in Azure SQL Database.](#BulkInsert) | 
 | ClrAssemblies | Database | Issue | [SQL CLR assemblies aren't supported in Azure SQL Database.](#ClrAssemblies) | 
 | ComputeClause | Database | Warning | [COMPUTE clause is no longer supported and has been removed.](#ComputeClause) | 
 | CrossDatabaseReferences | Database | Issue | [Cross-database queries aren't supported in Azure SQL Database.](#CrossDatabaseReferences) | 
 | CryptographicProvider | Database | Issue | [A use of CREATE CRYPTOGRAPHIC PROVIDER or ALTER CRYPTOGRAPHIC PROVIDER was found, which isn't supported in Azure SQL Database.](#CryptographicProvider) | 
 | DatabaseMail | Instance | Warning | [Database Mail isn't supported in Azure SQL Database.](#DatabaseMail) | 
 | DatabasePrincipalAlias | Database | Issue | [SYS.DATABASE_PRINCIPAL_ALIASES is no longer supported and has been removed.](#DatabasePrincipalAlias) | 
 | DbCompatLevelLowerThan100 | Database | Warning | [Azure SQL Database doesn't support compatibility levels below 100.](#DbCompatLevelLowerThan100) | 
 | DisableDefCNSTCHK | Database | Issue | [SET option DISABLE_DEF_CNST_CHK is no longer supported and has been removed.](#DisableDefCNSTCHK) | 
 | FastFirstRowHint | Database | Warning | [FASTFIRSTROW query hint is no longer supported and has been removed.](#FastFirstRowHint) | 
 | FileStream | Database | Issue | [Filestream isn't supported in Azure SQL Database.](#FileStream) | 
 | LinkedServer | Database | Issue | [Linked server functionality isn't supported in Azure SQL Database.](#LinkedServer) | 
 | MSDTCTransactSQL | Database | Issue | [BEGIN DISTRIBUTED TRANSACTION isn't supported in Azure SQL Database.](#MSDTCTransactSQL) | 
 | NextColumn | Database | Issue | [Tables and Columns named NEXT will lead to an error In Azure SQL Database.](#NextColumn) | 
 | NonANSILeftOuterJoinSyntax | Database | Warning | [Non-ANSI style left outer join is no longer supported and has been removed.](#NonANSILeftOuterJoinSyntax) | 
 | NonANSIRightOuterJoinSyntax | Database | Warning | [Non-ANSI style right outer join is no longer supported and has been removed.](#NonANSIRightOuterJoinSyntax) | 
 | OpenRowsetWithNonBlobDataSourceBulk | Database | Issue | [OpenRowSet used in bulk operation with non-Azure blob storage data source isn't supported in Azure SQL Database.](#OpenRowsetWithNonBlobDataSourceBulk) | 
 | OpenRowsetWithSQLAndNonSQLProvider | Database | Issue | [OpenRowSet with SQL or non-SQL provider isn't supported in Azure SQL Database.](#OpenRowsetWithSQLAndNonSQLProvider) | 
 | RAISERROR | Database | Warning | [Legacy style RAISERROR calls should be replaced with modern equivalents.](#RAISERROR) | 
 | ServerAudits | Instance | Warning | [Server Audits isn't supported in Azure SQL Database.](#ServerAudits) | 
 | ServerCredentials | Instance | Warning | [Server scoped credential isn't supported in Azure SQL Database.](#ServerCredentials) | 
 | ServerScopedTriggers | Instance | Warning  | [Server-scoped trigger isn't supported in Azure SQL Database.](#ServerScopedTriggers) | 
 | ServiceBroker | Database | Issue | [Service Broker feature isn't supported in Azure SQL Database.](#ServiceBroker) | 
 | SQLDBDatabaseSize | Database | Issue | [Azure SQL Database does not support database size greater than 100 TB.](#SQLDBDatabaseSize) | 
 | SqlMail | Database | Warning | [SQL Mail has been discontinued.](#SqlMail) | 
 | SystemProcedures110 | Database | Warning | [Detected statements that reference removed system stored procedures that aren't available in Azure SQL Database.](#SystemProcedures110) | 
 | TraceFlags | Instance | Warning | [Azure SQL Database does not support trace flags.](#TraceFlags) | 
 | WindowsAuthentication | Instance | Warning | [Database users mapped with Windows authentication (integrated security) aren't supported in Azure SQL Database.](#WindowsAuthentication) | 
 | XpCmdshell | Database | Issue | [xp_cmdshell isn't supported in Azure SQL Database.](#XpCmdshell) | 

## Bulk insert<a id="BulkInsert"></a>

**Title: BULK INSERT with non-Azure blob data source isn't supported in Azure SQL Database.**   
**Category**: Issue   

**Description**   
Azure SQL Database cannot access file shares or Windows folders. See the "Impacted Objects" section for the specific uses of BULK INSERT statements that do not reference an Azure blob. Objects with 'BULK INSERT' where the source isn't Azure Blob Storage will not work after migrating to Azure SQL Database. 


**Recommendation**   
You will need to convert BULK INSERT statements that use local files or file shares to use files from Azure Blob Storage instead, when migrating to Azure SQL Database. Alternatively, migrate to SQL Server on Azure Virtual Machine.

## Compute clause<a id="ComputeClause"></a>

**Title: COMPUTE clause is no longer supported and has been removed.**   
**Category**: Warning   

**Description**   
The COMPUTE clause generates totals that appear as additional summary columns at the end of the result set. However, this clause is no longer supported in Azure SQL Database. 


**Recommendation**   
The T-SQL module needs to be rewritten using the ROLLUP operator instead. The code below demonstrates how COMPUTE can be replaced with ROLLUP: 

```sql 
USE AdventureWorks2022;
GO;  

SELECT SalesOrderID, UnitPrice, UnitPriceDiscount 
FROM Sales.SalesOrderDetail 
ORDER BY SalesOrderID COMPUTE SUM(UnitPrice), SUM(UnitPriceDiscount) BY SalesOrderID GO; 

SELECT SalesOrderID, UnitPrice, UnitPriceDiscount,SUM(UnitPrice) as UnitPrice , 
SUM(UnitPriceDiscount) as UnitPriceDiscount 
FROM Sales.SalesOrderDetail 
GROUP BY SalesOrderID, UnitPrice, UnitPriceDiscount WITH ROLLUP; 
```

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## CLR assemblies<a id="ClrAssemblies"></a>

**Title: SQL CLR assemblies aren't supported in Azure SQL Database**   
**Category**: Issue   


**Description**   
Azure SQL Database does not support SQL CLR assemblies. 


**Recommendation**   
Currently, there is no way to achieve this in Azure SQL Database. The recommended alternative solutions will require application code and database changes to use only assemblies supported by Azure SQL Database. Alternatively migrate to Azure SQL Managed Instance or SQL Server on Azure Virtual Machine

More information: [Unsupported Transact-SQL differences in SQL Database](../../database/transact-sql-tsql-differences-sql-server.md#t-sql-syntax-not-supported-in-azure-sql-database)

## Cryptographic provider<a id="CryptographicProvider"></a>

**Title: A use of CREATE CRYPTOGRAPHIC PROVIDER or ALTER CRYPTOGRAPHIC PROVIDER was found, which isn't supported in Azure SQL Database**   
**Category**: Issue   

**Description**   
Azure SQL Database does not support CRYPTOGRAPHIC PROVIDER statements because it cannot access files. See the Impacted Objects section for the specific uses of CRYPTOGRAPHIC PROVIDER statements. Objects with `CREATE CRYPTOGRAPHIC PROVIDER` or `ALTER CRYPTOGRAPHIC PROVIDER` will not work correctly after migrating to Azure SQL Database.  


**Recommendation**   
Review objects with `CREATE CRYPTOGRAPHIC PROVIDER` or `ALTER CRYPTOGRAPHIC PROVIDER`. In any such objects that are required, remove the uses of these features. Alternatively, migrate to SQL Server on Azure Virtual Machine

## Cross database references<a id="CrossDatabaseReferences"></a>

**Title: Cross-database queries aren't supported in Azure SQL Database**   
**Category**: Issue   

**Description**   
Databases on this server use cross-database queries, which aren't supported in Azure SQL Database. 


**Recommendation**   
Azure SQL Database does not support cross-database queries. The following actions are recommended: 
- Migrate the dependent database(s) to Azure SQL Database and use Elastic Database Query (Currently in preview) functionality to query across Azure SQL databases. 
- Move the dependent datasets from other databases into the database that is being migrated. 
- Migrate to Azure SQL Managed Instance.
- Migrate to SQL Server on Azure Virtual Machine. 

More information: [Check Azure SQL Database elastic database query (Preview)](../../database/elastic-query-overview.md)

## Database compatibility<a id="DbCompatLevelLowerThan100"></a>

**Title: Azure SQL Database doesn't support compatibility levels below 100.**   
**Category**: Warning   

**Description**   
Database compatibility level is a valuable tool to assist in database modernization, by allowing the SQL Server Database Engine to be upgraded, while keeping connecting applications functional status by maintaining the same pre-upgrade database compatibility level. Azure SQL Database doesn't support compatibility levels below 100. 


**Recommendation**   
Evaluate if the application functionality is intact when the database compatibility level is upgraded to 100 on Azure SQL Managed Instance. Alternatively, migrate to SQL Server on Azure Virtual Machine

## Database mail<a id="DatabaseMail"></a>

**Title: Database Mail isn't supported in Azure SQL Database.**   
**Category**: Warning   

**Description**   
This server uses the Database Mail feature, which isn't supported in Azure SQL Database.


**Recommendation**   
Consider migrating to Azure SQL Managed Instance that supports Database Mail.  Alternatively, consider using Azure functions and Sendgrid to accomplish mail functionality on Azure SQL Database.

## Database principal alias<a id="DatabasePrincipalAlias"></a>

**Title: SYS.DATABASE_PRINCIPAL_ALIASES is no longer supported and has been removed.**   
**Category**: Issue   

**Description**   
SYS.DATABASE_PRINCIPAL_ALIASES is no longer supported and has been removed in Azure SQL Database.  


**Recommendation**   
Use roles instead of aliases.

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)


## DISABLE_DEF_CNST_CHK option<a id="DisableDefCNSTCHK"></a>

**Title: SET option DISABLE_DEF_CNST_CHK is  discontinued and has been removed.**   
**Category**: Issue   

**Description**   
SET option DISABLE_DEF_CNST_CHK is  discontinued and has been removed in Azure SQL Database.  


More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## FASTFIRSTROW hint<a id="FastFirstRowHint"></a>

**Title: FASTFIRSTROW query hint is no longer supported and has been removed.**   
**Category**: Warning   

**Description**   
FASTFIRSTROW query hint is no longer supported and has been removed in Azure SQL Database.  


**Recommendation**   
Instead of FASTFIRSTROW query hint use OPTION (FAST n).

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## FileStream<a id="FileStream"></a>

**Title: Filestream isn't supported in Azure SQL Database**   
**Category**: Issue   

**Description**   
The Filestream feature, which allows you to store unstructured data such as text documents, images, and videos in NTFS file system, isn't supported in Azure SQL Database. 


**Recommendation**   
Upload the unstructured files to Azure Blob storage and store metadata related to these files (name, type, URL location, storage key etc.) in Azure SQL Database. You may have to re-engineer your application to enable streaming blobs to and from Azure SQL Database. Alternatively, migrate to SQL Server on Azure Virtual Machine.

More information: [Streaming blobs to and from Azure SQL blog](https://azure.microsoft.com/blog/streaming-blobs-to-and-from-sql-azure/)


## Linked server<a id="LinkedServer"></a>

**Title: Linked server functionality isn't supported in Azure SQL Database**   
**Category**: Issue   

**Description**   
Linked servers enable the SQL Server Database Engine to execute commands against OLE DB data sources outside of the instance of SQL Server. 


**Recommendation**   
Azure SQL Database does not support linked server functionality. The following actions are recommended to eliminate the need for linked servers: 
- Identify the dependent datasets from remote SQL servers and consider moving these into the database being migrated. 
- Migrate the dependent database(s) to Azure and use Elastic Database Query (preview) functionality to query across databases in Azure SQL Database. 

More information: [Check Azure SQL Database elastic query (Preview)](../../database/elastic-query-overview.md) 

## MS DTC<a id="MSDTCTransactSQL"></a>

**Title: BEGIN DISTRIBUTED TRANSACTION isn't supported in Azure SQL Database.**   
**Category**: Issue   

**Description**   
Distributed transaction started by Transact SQL BEGIN DISTRIBUTED TRANSACTION and managed by Microsoft Distributed Transaction Coordinator (MS DTC) isn't supported in Azure SQL Database.  


**Recommendation**   
Review impacted objects section in Azure Migrate to see all objects using BEGIN DISTRUBUTED TRANSACTION. Consider migrating the participant databases to Azure SQL Managed Instance where distributed transactions across multiple instances are supported. For more information, see [Transactions across multiple servers for Azure SQL Managed Instance](../../database/elastic-transactions-overview.md#transactions-for-sql-managed-instance). 

Alternatively, migrate to SQL Server on Azure Virtual Machine.

## OPENROWSET (bulk)<a id="OpenRowsetWithNonBlobDataSourceBulk"></a>

**Title: OpenRowSet used in bulk operation with non-Azure blob storage data source isn't supported in Azure SQL Database.**   
**Category**: Issue   

**Description**
OPENROWSET supports bulk operations through a built-in BULK provider that enables data from a file to be read and returned as a rowset. OPENROWSET with non-Azure blob storage data source isn't supported in Azure SQL Database.


**Recommendation**   
Azure SQL Database cannot access file shares and Windows folders, so the files must be imported from Azure Blob Storage. Therefore, only blob type DATASOURCE is supported in OPENROWSET function. Alternatively, migrate to SQL Server on Azure Virtual Machine

More information: [Resolving Transact-SQL differences during migration to SQL Database](../../database/transact-sql-tsql-differences-sql-server.md#t-sql-syntax-not-supported-in-azure-sql-database)


## OPENROWSET (provider)<a id="OpenRowsetWithSQLAndNonSQLProvider"></a>

**Title: OpenRowSet with SQL or non-SQL provider isn't supported in Azure SQL Database.**   
**Category**: Issue   

**Description**   
OpenRowSet with SQL or non-SQL provider is an alternative to accessing tables in a linked server and is a one-time, ad hoc method of connecting and accessing remote data by using OLE DB. OpenRowSet with SQL or non-SQL provider isn't supported in Azure SQL Database.


**Recommendation**   
Azure SQL Database supports OPENROWSET only to import from Azure Blob Storage. Alternatively, migrate to SQL Server on Azure Virtual Machine

More information: [Resolving Transact-SQL differences during migration to SQL Database](../../database/transact-sql-tsql-differences-sql-server.md#t-sql-syntax-not-supported-in-azure-sql-database)


## Non-ANSI left outer join<a id="NonANSILeftOuterJoinSyntax"></a>

**Title: Non-ANSI style left outer join is no longer supported and has been removed.**   
**Category**: Warning   

**Description**   
Non-ANSI style left outer join is no longer supported and has been removed in Azure SQL Database. 


**Recommendation**   
Use ANSI join syntax.

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)


## Non-ANSI right outer join<a id="NonANSIRightOuterJoinSyntax"></a>

**Title: Non-ANSI style right outer join is no longer supported and has been removed.**   
**Category**: Warning   

**Description**   
Non-ANSI style right outer join is no longer supported and has been removed in Azure SQL Database. 


**Recommendation**   
Use ANSI join syntax.

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## Next column<a id="NextColumn"></a>

**Title: Tables and Columns named NEXT will lead to an error In Azure SQL Database.**   
**Category**: Issue   

**Description**   
Tables or columns named NEXT were detected. Sequences, introduced in Microsoft SQL Server, use the ANSI standard NEXT VALUE FOR function. If a table or a column is named NEXT and the column is aliased as VALUE, and if the ANSI standard AS is omitted, the resulting statement can cause an error.  


**Recommendation**   
Rewrite statements to include the ANSI standard AS keyword when aliasing a table or column. For example, when a column is named NEXT and that column is aliased as VALUE, the query `SELECT NEXT VALUE FROM TABLE` will cause an error and should be rewritten as SELECT NEXT AS VALUE FROM TABLE. Similarly, when a table is named NEXT and that table is aliased as VALUE, the query `SELECT Col1 FROM NEXT VALUE` will cause an error and should be rewritten as `SELECT Col1 FROM NEXT AS VALUE`.

## RAISERROR<a id="RAISERROR"></a>

**Title: Legacy style RAISERROR calls should be replaced with modern equivalents.**   
**Category**: Warning   

**Description**   
RAISERROR calls like the below example are termed as legacy-style because they do not include the commas and the parenthesis. `RAISERROR 50001 'this is a test'`. This method of calling RAISERROR is no longer supported and removed in Azure SQL Database. 


**Recommendation**   
Rewrite the statement using the current RAISERROR syntax, or evaluate if the modern  approach of `BEGIN TRY { }  END TRY BEGIN CATCH {  THROW; } END CATCH` is feasible.

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## Server audits<a id="ServerAudits"></a>

**Title: Use Azure SQL Database audit features to replace Server Audits**   
**Category**: Warning   

**Description**   
Server Audits isn't supported in Azure SQL Database.


**Recommendation**   
Consider Azure SQL Database audit features to replace Server Audits.  Azure SQL supports audit and the features are richer than SQL Server. Azure SQL Database can audit various database actions and events, including: Access to data, Schema changes (DDL), Data changes (DML), Accounts, roles, and permissions (DCL, Security exceptions. Azure SQL Database Auditing increases an organization's ability to gain deep insight into events and changes that occur within their database, including updates and queries against the data. Alternatively migrate to Azure SQL Managed Instance or SQL Server on Azure Virtual Machine.

More information: [Auditing for Azure SQL Database](../../database/auditing-overview.md)

## Server credentials<a id="ServerCredentials"></a>

**Title: Server scoped credential isn't supported in Azure SQL Database**   
**Category**: Warning   

**Description**   
A credential is a record that contains the authentication information (credentials) required to connect to a resource outside SQL Server. Azure SQL Database supports database credentials, but not the ones created at the SQL Server scope.   


**Recommendation**   
Azure SQL Database supports database scoped credentials. Convert server scoped credentials to database scoped credentials. Alternatively migrate to Azure SQL Managed Instance or SQL Server on Azure Virtual Machine

More information: [Creating database scoped credential](/sql/t-sql/statements/create-database-scoped-credential-transact-sql)

## Service Broker<a id="ServiceBroker"></a>

**Title: Service Broker feature isn't supported in Azure SQL Database**   
**Category**: Issue   

**Description**   
SQL Server Service Broker provides native support for messaging and queuing applications in the SQL Server Database Engine. Service Broker feature isn't supported in Azure SQL Database.


**Recommendation**   
Service Broker feature isn't supported in Azure SQL Database. Consider migrating to Azure SQL Managed Instance that supports service broker within the same instance. Alternatively, migrate to SQL Server on Azure Virtual Machine. 

## Server-scoped triggers<a id="ServerScopedTriggers"></a>

**Title: Server-scoped trigger isn't supported in Azure SQL Database**   
**Category**: Warning   

**Description**   
A trigger is a special kind of stored procedure that executes in response to certain action on a table like insertion, deletion, or updating of data. Server-scoped triggers aren't supported in Azure SQL Database. Azure SQL Database does not support the following options for triggers: FOR LOGON, ENCRYPTION, WITH APPEND, NOT FOR REPLICATION, EXTERNAL NAME option (there is no external method support), ALL SERVER Option (DDL Trigger), Trigger on a LOGON event (Logon Trigger), Azure SQL Database does not support CLR-triggers.


**Recommendation**   
Use database level trigger instead. Alternatively migrate to Azure SQL Managed Instance or SQL Server on Azure Virtual Machine

More information: [Resolving Transact-SQL differences during migration to SQL Database](../../database/transact-sql-tsql-differences-sql-server.md#t-sql-syntax-not-supported-in-azure-sql-database)


## SQL Agent jobs<a id="AgentJobs"></a>

**Title: SQL Server Agent jobs aren't available in Azure SQL Database**   
**Category**: Warning   

**Description**   
SQL Server Agent is a Microsoft Windows service that executes scheduled administrative tasks, which are called jobs in SQL Server. SQL Server Agent jobs aren't available in Azure SQL Database. 


**Recommendation** 
Use elastic jobs (preview), which are the replacement for SQL Server Agent jobs in Azure SQL Database. Elastic Database jobs for Azure SQL Database allow you to reliably execute T-SQL scripts that span multiple databases while automatically retrying and providing eventual completion guarantees. Alternatively consider migrating to  Azure SQL Managed Instance or SQL Server on Azure Virtual Machines.

More information: [Getting started with Elastic Database jobs (Preview)](../../database/elastic-jobs-overview.md)

## SQL Database size<a id="SQLDBDatabaseSize"></a>

**Title: Azure SQL Database does not support database size greater than 100 TB.**   
**Category**: Issue   

**Description**   
The size of the database is greater than the maximum supported size of 100 TB. 


**Recommendation**   
Evaluate if the data can be archived or compressed or sharded into multiple databases. Alternatively, migrate to SQL Server on Azure Virtual Machine. 

More information: [vCore resource limits](../../database/resource-limits-vcore-single-databases.md) 

## SQL Mail<a id="SqlMail"></a>

**Title: SQL Mail has been discontinued.**   
**Category**: Warning   

**Description**   
SQL Mail has been discontinued and removed in Azure SQL Database.


**Recommendation**   
Consider migrating to Azure SQL Managed Instance or SQL Server on Azure Virtual Machines and use Database Mail.

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## SystemProcedures110<a id="SystemProcedures110"></a>

**Title: Detected statements that reference removed system stored procedures that aren't available in Azure SQL Database.**   
**Category**: Warning   

**Description**   
Following unsupported system and extended stored procedures cannot be used in Azure SQL Database - `sp_dboption`, `sp_addserver`, `sp_dropalias`,`sp_activedirectory_obj`, `sp_activedirectory_scp`, `sp_activedirectory_start`.


**Recommendation**    
Remove references to unsupported system procedures that have been removed in Azure SQL Database.

More information: [Discontinued Database Engine functionality in SQL Server](/previous-versions/sql/2014/database-engine/discontinued-database-engine-functionality-in-sql-server-2016#Denali)

## Trace flags<a id="TraceFlags"></a>

**Title: Azure SQL Database does not support trace flags**   
**Category**: Warning   

**Description**   
Trace flags are used to temporarily set specific server characteristics or to switch off a particular behavior. Trace flags are frequently used to diagnose performance issues or to debug stored procedures or complex computer systems. Azure SQL Database does not support trace flags. 


**Recommendation**   
Review impacted objects section in Azure Migrate to see all trace flags that aren't supported in Azure SQL Database and evaluate if they can be removed. Alternatively, migrate to Azure SQL Managed Instance which supports limited number of global trace flags or SQL Server on Azure Virtual Machine.

More information: [Resolving Transact-SQL differences during migration to SQL Database](../../database/transact-sql-tsql-differences-sql-server.md#t-sql-syntax-not-supported-in-azure-sql-database)


## Windows authentication<a id="WindowsAuthentication"></a>

**Title: Database users mapped with Windows authentication (integrated security) aren't supported in Azure SQL Database.**   
**Category**: Warning   

**Description**   
Azure SQL Database supports two types of authentication 
- SQL Authentication: uses a username and password 
- Azure Active Directory Authentication:  uses identities managed by Azure Active Directory and is supported for managed and integrated domains. 

Database users mapped with Windows authentication (integrated security) aren't supported in Azure SQL Database. 



**Recommendation**   
Federate the local Active Directory with Azure Active Directory. The Windows identity can then be replaced with the equivalent Azure Active Directory identities. Alternatively, migrate to SQL Server on Azure Virtual Machine.

More information: [SQL Database security capabilities](../../database/security-overview.md#authentication)

## XP_cmdshell<a id="XpCmdshell"></a>

**Title: xp_cmdshell isn't supported in Azure SQL Database.**   
**Category**: Issue   

**Description**   
xp_cmdshell which spawns a Windows command shell and passes in a string for execution isn't supported in Azure SQL Database. 


**Recommendation**   
Review impacted objects section in Azure Migrate to see all objects using xp_cmdshell and evaluate if the reference to xp_cmdshell or the impacted object can be removed. Also consider exploring Azure Automation that delivers cloud-based automation and configuration service. Alternatively, migrate to SQL Server on Azure Virtual Machine. 

## Next steps

To start migrating your SQL Server to Azure SQL Database, see the [SQL Server to SQL Database migration guide](sql-server-to-sql-database-guide.md).

- For a matrix of available Microsoft and third-party services and tools to assist you with various database and data migration scenarios as well as specialty tasks, see [Service and tools for data migration](/azure/dms/dms-tools-matrix).

- To learn more about SQL Database, see:
   - [Overview of Azure SQL Database](../../database/sql-database-paas-overview.md)
   - [Azure total Cost of Ownership Calculator](https://azure.microsoft.com/pricing/tco/calculator/) 

- To learn more about the framework and adoption cycle for Cloud migrations, see
   -  [Cloud Adoption Framework for Azure](/azure/cloud-adoption-framework/migrate/azure-best-practices/contoso-migration-scale)
   -  [Best practices for costing and sizing workloads migrate to Azure](/azure/cloud-adoption-framework/migrate/azure-best-practices/migrate-best-practices-costs) 


- To assess the Application access layer, see [Data Access Migration Toolkit (Preview)](https://marketplace.visualstudio.com/items?itemName=ms-databasemigration.data-access-migration-toolkit)
- For details on how to perform Data Access Layer A/B testing see [Database Experimentation Assistant](/sql/dea/database-experimentation-assistant-overview).
