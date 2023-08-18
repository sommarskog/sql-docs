---
title: DacFx and SqlPackage release notes
description: Release notes for Microsoft SqlPackage.
author: dzsquared
ms.author: drskwier
ms.reviewer: "llali"
ms.date: 5/10/2023
ms.service: sql
ms.topic: conceptual
ms.custom: tools|sos
---
# Release notes for SqlPackage

**[Download the latest version](sqlpackage-download.md)**

This article lists the features and fixes delivered by the released versions of SqlPackage.


## 162.0.52 SqlPackage

**Release date:** May 11, 2023

|Platform|Download|Version|
|:---|:---|:---|
|Windows .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2236505)|162.0.52|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2236347)|162.0.52|
|macOS .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2236426)|162.0.52|
|Linux .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2236425)|162.0.52|


### Features
| Feature | Details |
| :------ | :------ |
|Platform|SqlPackage now collects usage data, including anonymous feature usage and diagnostic data. For more information, see [Usage data collection](sqlpackage.md#usage-data-collection).|
|Platform|References [Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/5.1.0) v5.1.0|
|Azure Synapse Analytics|Adds support for [DW_COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md#dw_compatibility_level---auto--10--20--30--40--50--9000-).|
|ScriptDOM|ScriptDOM is now available as a standalone package on [NuGet](https://www.nuget.org/packages/Microsoft.SqlServer.TransactSql.ScriptDom) and is open source on [GitHub](https://github.com/microsoft/SqlScriptDOM).|
|System dacpacs|The `master` and `msdb` system dacpacs are now available on NuGet as [Microsoft.SqlServer.Dacpacs.Master](https://www.nuget.org/packages/Microsoft.SqlServer.Dacpacs.Master) and [Microsoft.SqlServer.Dacpacs.Msdb](https://www.nuget.org/packages/Microsoft.SqlServer.Dacpacs.Msdb). More information on the system dacpacs and consuming dacpacs as a package reference is available in the [DacFx GitHub repository](https://github.com/microsoft/DacFx).|

### Fixes
| Feature | Details |
| :------ | :------ |
|Azure Synapse Analytics|Fixes an issue where the default command timeout was not set properly when connecting to Azure Synapse Analytics serverless SQL pools.|
|Azure Synapse Analytics|Fixes an issue where Azure Synapse Analytics serverless SQL pools would incorrectly determine the default data and log paths.|
|Azure Synapse Analytics|Fixes an issue where Azure Synapse Analytics serverless SQL pools would incorrectly determine the default login, user and schema.|
|Azure SQL Database|Fixes an issue where temporal history retention was not correctly recognized as not configured (null).|
|Deployment|Fixes an issue where the deployment plan fails to detect a dependency on a table/view in subqueries within FROM VALUES clause. [GitHub issue](https://github.com/microsoft/DacFx/issues/156)|
|Deployment|Fixes an issue where deployment would fail when the target database contains a rule bound to a column.|
|Deployment|Fixes an issue where deployment would fail when the target database contains a rule bound to a column with a user-defined type. [GitHub issue](https://github.com/microsoft/DacFx/issues/245)|
|Deployment|Fixes an issue where the retention period on a temporal table would be reset to the default value when another change is made to the table. [GitHub issue](https://github.com/microsoft/DacFx/issues/258)|
|Deployment|Fixes an issue where updates to a primary key is not included in the deployment when the table has compression options specified.|
|Deployment|Fixes an issue where a non-clustered index on a partitioned table is rebuilt even when no changes are made to the table. [GitHub issue](https://github.com/microsoft/DacFx/issues/202)|
|Deployment|Fixes an issue where ignorecolumnorder property is not honored by a history table when no changes are made to a system-versioned table except the columns are reordered.|
|Deployment|Fixes an issue where external tables would be dropped and redeployed despite no changes when the table definition contained SQLCMD variables. [GitHub issue](https://github.com/microsoft/DacFx/issues/249)|
|Export|Fixes an issue where the diagnostic information provided during an export operation incorrectly reports the size of a table in KB instead of Bytes. [GitHub issue](https://github.com/microsoft/DacFx/issues/209)|
|Import|Fixes an issue where an Azure Active Directory user cannot be created during import to Azure SQL Database, causing the import to fail. [GitHub issue](https://github.com/microsoft/DacFx/issues/260)|
|Ledger|Fixes an issue where SqlPackage was not correctly identifying the error when the Ledger history table or view have an invalid two-part name.|
|Permissions|Fixes an issue where permissions assigned to a user in the database model are not recognized, causing the project build or SqlPackage operation to fail.|
|Query Store|Fixes an issue where the `flush_interval_seconds` [Query Store option](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md) was not correctly validated with a minimum value of 60 seconds.|
|SQL Server 2022|Fixes an issue where the function `DATETRUNC` was not recognized as a built-in function. [Developer Community report](https://developercommunity.visualstudio.com/t/Visual-Studio-build-solution-not-recogni/10333180)|
|SQL Server 2022|Fixes an issue where the function `DATE_BUCKET` was not recognized as a built-in function.|


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |

## 161.8089.0 SqlPackage

**Release date:** February 13, 2023

|Platform|Download|Version|Build
|:---|:---|:---|:---|
|Windows .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2224909)|161.8089.0|16.1.8089.0|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2224908)|161.8089.0|16.1.8089.0|
|macOS .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2225106)|161.8089.0|16.1.8089.0|
|Linux .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2225105)|161.8089.0|16.1.8089.0|

> [!IMPORTANT]
> Version 161 of SqlPackage encrypts database connections by default. Previously successful connections with self-signed certificates or without encryption may not connect with v161 without updating the SqlPackage parameters.  For more information, see [https://aka.ms/dacfx-connection](https://aka.ms/dacfx-connection).


### Features
| Feature | Details |
| :------ | :------ |
|Deployment|Adds the ability for the `GenerateSmartDefaults` property on publish to populate values from a default constraint when set to `true`. [GitHub issue](https://github.com/microsoft/DacFx/issues/38)|
|Azure Synapse Analytics|Adds support for [serverless SQL pools](./sqlpackage-for-azure-synapse-analytics.md#support-for-serverless-sql-pools) in Extract and Publish operations.|
|SQL Server 2022|Adds support for [ordered clustered columnstore indexes](../../relational-databases/indexes/columnstore-indexes-design-guidance.md#use-an-ordered-clustered-columnstore-index-for-large-data-warehouse-tables).|


### Fixes
| Feature | Details |
| :------ | :------ |
|Deployment|Fixes an issue where publish to SQL on Linux would fail due to the default data and log paths being empty. [GitHub issue](https://github.com/microsoft/DacFx/issues/136)|
|Deployment|Fixes an issue where publishing an external table with file format changes would result in an error. [GitHub issue](https://github.com/microsoft/DacFx/issues/120)|
|Deployment|Fixes an issue where publish with a column encrypted with randomized encryption would not fail immediately if the column encryption key (CEK) was inaccessible, delaying the deployment error until the column encryption step.|
|Refactor|Fixes an issue where a renamed column on a system versioned table would result in the system versioning being turned off and not turned back on. [GitHub issue](https://github.com/microsoft/DacFx/issues/203)|
|Platform|Fixes an issue where SqlPackage operations would fail on RHEL 9 due to an encryption error. Moves to use the 6.0.10 version of the .NET 6 runtime. [GitHub issue](https://github.com/microsoft/DacFx/issues/168)|
|Schema compare|Fixes an issue where the `DoNotEvaluateSqlCmdVariables` property for *Publish* and *Script* would result in the SqlCmd variables also not being evaluated on both the source and target instead of only the source.|
|ScriptDOM|Fixes external table support for `REJECT_SAMPLE_VALUE`.|
|ScriptDOM|Fixes an issue where compression options could not be applied to a table with a clustered index.|
|SQL projects|Fixes an issue where valid options for the `QueryStoreFlushInterval` are incorrectly reported as invalid. [Developer Community report](https://developercommunity.visualstudio.com/t/SQL72003:-The-value-300-for-property-Que/10210937)|

### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |

## 161.6374.0 SqlPackage

**Release date:** November 9, 2022

|Platform|Download|Version|Build
|:---|:---|:---|:---|
|Windows .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2215400)|161.6374.0|16.1.6374.0|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2215326)|161.6374.0|16.1.6374.0|
|macOS .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2215401)|161.6374.0|16.1.6374.0|
|Linux .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2215501)|161.6374.0|16.1.6374.0|

> [!IMPORTANT]
> Version 161 of SqlPackage encrypts database connections by default. Previously successful connections with self-signed certificates or without encryption may not connect with v161 without updating the SqlPackage parameters.  For more information, see [https://aka.ms/dacfx-connection](https://aka.ms/dacfx-connection).

### Features
| Feature | Details |
| :------ | :------ |
|Platform|Changes connections to use encryption and not trust the server certificate by default. This is a breaking change for connections using self-signed certificates or without encryption by default.  For more information, see [this dedicated article](https://aka.ms/dacfx-connection).|
|Platform|References [Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/5.0.1) v5.0.1|
|Platform|SqlPackage is now available for [installation](sqlpackage-download.md) as a `dotnet tool` for Windows, macOS, and Linux platforms.|
|Always Encrypted|Adds support for VBS (Virtualization-based security) with [secure enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves.md).|
|Connectivity|Adds support for TDS 8.0 and parameters for `/SourceHostNameInCertificate` and `/TargetHostNameInCertificate` to SqlPackage operations.|
|Replication|Adds support for [sp_addpublication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md#automatically-handle-conflicts-with-last-write-wins) with peer-to-peer replication.|
|ScriptDOM|Adds support for IS NOT DISTINCT FROM syntax with predicate subqueries.|
|Server-level roles|Adds support for additional [fixed server roles](../../relational-databases/security/authentication-access/server-level-roles.md#fixed-server-level-roles-introduced-in-sql-server-2022): MS_DatabaseConnector, MS_LoginManager, MS_DatabaseManager, MS_ServerStateManager, MS_ServerStateReader, MS_ServerPerformanceStateReader, MS_ServerSecurityStateReader, MS_DefinitionReader, MS_PerformanceDefinitionReader, MS_SecurityDefinitionReader.|
|SQL Server 2022|Adds support for [T-SQL function changes associated with SQL Server 2022](../../sql-server/what-s-new-in-sql-server-2022.md#language): GREATEST(), LEAST(), STRING_SPLIT(), DATETRUNC(), LTRIM(), RTRIM(), and TRIM().|
|SQL Server 2022|Adds support for [JSON function changes associated with SQL Server 2022](../../sql-server/what-s-new-in-sql-server-2022.md#language): ISJSON(), JSON_PATH_EXISTS(), JSON_OBJECT(), and JSON_ARRAY().|
|SQL Server 2022|Adds support for [bit manipulation functions associated with SQL Server 2022](../../t-sql/functions/bit-manipulation-functions-overview.md): LEFT_SHIFT(), RIGHT_SHIFT(), BIT_COUNT(), GET_BIT(), and SET_BIT().|
|SQL Server 2022|Adds support for [time series function changes associated with SQL Server 2022](../../sql-server/what-s-new-in-sql-server-2022.md#language): DATE_BUCKET(), GENERATE_SERIES(), FIRST_VALUE(), and LAST_VALUE().|
|Statistics|Adds support for [STATISTICS AUTO_DROP option](../../t-sql/statements/create-statistics-transact-sql.md).|
|XML compression|Adds support for XML compression on [XML indexes](../../relational-databases/xml/xml-indexes-sql-server.md#xml-compression).|


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |

## 19.2 SqlPackage

**Release date:** September 22, 2022

|Platform|Download|Version|Build
|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2209512)|19.2|16.0.6296.0|
|macOS .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2209610)| 19.2|16.0.6296.0|
|Linux .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2209513)| 19.2|16.0.6296.0|
|Windows .NET 6 |[.zip file](https://go.microsoft.com/fwlink/?linkid=2209609)| 19.2|16.0.6296.0|


### Features
| Feature | Details |
| :------ | :------ |
| Connection pooling | Enables connection pooling for all connections if the environment variable `CONNECTION_POOLING_ENABLED` is set to True.  This is recommended for operations with Azure Active Directory username/password connections to avoid MSAL throttling. |
| Deployment options | Surfaces friendly names for deployment options in DacFx .NET APIs. |
| Dynamic Data Masking | Adds support for [granular UNMASK permissions](../../relational-databases/security/dynamic-data-masking.md#granular) in Import/Export and Extract/Publish.|
| Ledger | Adds SQL Ledger history table in schema model for validation and export/extract, does not import or publish the history table to a database. |
| Platform | SqlPackage is now built with .NET 6 |
| SQL Server 2022 | Adds support for permissions ALTER LEDGER CONFIGURATION, VIEW PERFORMANCE DEFINITION, VIEW ANY PERFORMANCE DEFINITION. Learn more about the permission definitions available in the [permissions documentation](../../relational-databases/security/permissions-database-engine.md).|
| XML compression | [XML compression](../../t-sql/statements/create-table-transact-sql.md#xml_compression) support in ScriptDOM, Import/Export, and Extract/Publish. More information on XML data and XML compression is available in the [XML data documentation](../../relational-databases/xml/xml-data-sql-server.md). |


### Fixes
| Feature | Details |
| :------ | :------ |
| Export | Fixes an issue where export would fail when a table had stats with computed columns |
| Import | Fixes an issue where the import would get stuck at 95% |
| ScriptDOM | Fixes an issue where STRING_SPLIT would not support a NULL ordinal value |


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |
| XML compression | XML compression of an XML index is not yet supported in SqlPackage. | N/A |

## 19.1 SqlPackage

**Release date:** May 24, 2022

|Platform|Download|Version|Build
|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2196438)|19.1|16.0.6161.0|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2196439)| 19.1|16.0.6161.0|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2196335)| 19.1|16.0.6161.0|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2196334)| 19.1|16.0.6161.0|


### Features
| Feature | Details |
| :------ | :------ |
| Azure Synapse Analytics | Adds support for [Native external data source](/azure/synapse-analytics/sql/develop-tables-external-tables?tabs=native#syntax-for-create-external-data-source). |
| Extract | Adds support for `ExtractTarget` property on extract operations.  Extract now supports extracting to .sql as a file per object organized in a single folder, object type, schema, or object type and schema. |
| ScriptDOM | Adds support for `IS NOT DISTINCT FROM` syntax. |



### Fixes
| Feature | Details |
| :------ | :------ |
| Azure Synapse Analytics | Fixes publish operation for table name change where table name includes '/' character. |
| Export | Fixes export of a SQL ledger history table with dependencies. |
| Extract | Fixes extract operation failure where an offset clause using a function is used in a stored procedure. |
| Extract | Fixes warnings on extract operation for ledger tables. |
| General | Fixes issue where command timeout setting was not properly applied. |
| Import | Fixes issue where full text index gets disabled on import. |
| Publish | Fixes issue where publish operation would drop and create a clustered columnstore index when a column is added. |
| Publish | Fixes issue where graph tables fail to deploy when a partition function includes leading zeros. |
| ScriptDOM | Fixes an issue where `IIF` condition is enclosed in parenthesis fails to parse. |


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| Deployment | Increased deployment time when deploying using Azure Active Directory user/password authentication due to MSAL throttling. [More Information on GitHub](https://github.com/microsoft/DacFx/issues/92) | Use an alternative authentication method, such as [Azure Active Directory Service Principal](/azure/azure-sql/database/authentication-aad-service-principal)|
|Deployment|SqlPackage on .NET Core for Windows, macOS, and Linux fails during a publish operation with an error message "Unrecognized configuration section system.diagnostics" when in-place encryption is used for Always Encrypted with secure enclaves.|Remove the file `sqlpackage.dll.config` from the SqlPackage folder.|
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |


## 19.0 SqlPackage

**Release date:** January 25, 2022

|Platform|Download|Version|Build
|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2185764)|19.0|16.0.5400.1|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2185765)| 19.0|16.0.5400.1|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2185670)| 19.0|16.0.5400.1|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2185669)| 19.0|16.0.5400.1|


### Features
| Feature | Details |
| :------ | :------ |
|Always Encrypted|Adds support for in-place encryption for Always Encrypted columns. Publish can now leverage a server-side secure enclave to encrypt, decrypt, and re-encrypt database columns in-place. This avoids the expense of moving the data outside of the database. See pre-requisites for in-place encryption in [Configure column encryption in-place using Always Encrypted with secure enclaves](../../relational-databases/security/encryption/always-encrypted-enclaves-configure-encryption.md). Note: In-place encryption is supported only with the offline approach. |
|Azure Synapse Analytics|Adds support for column-level symmetric encryption.|
|Ledger|Adds supports for exporting and importing databases with ledger tables. The following limitations apply to Export: Ledger history tables and dropped ledger tables aren't migrated; the values of `GENERATED ALWAYS` columns and the data in ledger system views isn't migrated; the value of the database-level Ledger property is ignored.|
|Platform|Adds support for .NET 6 as the target framework|
|Platform|References Microsoft.Data.SqlClient (3.0) instead of System.Data.SqlClient in .NET Framework version. Upgrade Microsoft.Data.SqlClient from 2.1.3 to 3.0 for .NET Core version.|
|Platform|Upgrades .NET Framework target version to .NET 4.6.2|
|ScriptDOM|Adds support for Sql160 parser.|



### Fixes
| Feature | Details |
| :------ | :------ |
| Deployment |Fixes issue with interpretation of table distribution on column within a stored procedure. |
| Deployment |Fixes issue with "Drop objects not in source" option during publish operation. |
| Deployment |Fixes for Deploying a dacpac with temporal table having sensitivity classification.  |
| Deployment |Fixes a bug when variables are verified even when DoNotEvaluateSqlCmdVariables is set to true|
| Extract |Fix for Refactor log of referenced dacpac according to includeCompositeObjects selection. |
| Import |Fixes issue with importing database scope configurations that are not supported in target server|
| SQL Project |Fixes issue where incremental statistics caused an issue with the project build when applied to a primary key. |
| SQL Project |Fixes building a project with file tables. |


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported. | N/A |
| Deployment | Increased deployment time when deploying using Azure Active Directory user/password authentication due to MSAL throttling. [More Information on GitHub](https://github.com/microsoft/DacFx/issues/92) | Use an alternative authentication method, such as [Azure Active Directory Service Principal](/azure/azure-sql/database/authentication-aad-service-principal)|
| ScriptDOM | Parsing a very large file can result in a stack overflow. | None |


## 18.8 SqlPackage

**Release date:** October 4, 2021

|Platform|Download|Version|Build
|:---|:---|:---|:---|
|Windows|[MSI Installer](https://go.microsoft.com/fwlink/?linkid=2164920)|18.8|15.0.5282.3|
|macOS .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165009)| 18.8|15.0.5282.3|
|Linux .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165008)| 18.8|15.0.5282.3|
|Windows .NET Core |[.zip file](https://go.microsoft.com/fwlink/?linkid=2165007)| 18.8|15.0.5282.3|


### Features
| Feature | Details |
| :------ | :------ |
| Export | Adds option VerifyExtraction to change behavior of schema model validation on export |
| Azure SQL | Support for ledger database and tables, including import and export actions. |
| Platform | Upgrade Microsoft.Data.SqlClient from 2.0.0 to 2.1.3 for .NET Core version |
| Azure Synapse Analytics | Support for column encryption with symmetric key  |
| Azure Synapse Analytics | Support for column encryption with CREATE CERTIFICATE |
| Azure Synapse Analytics | Support for MERGE statement |
| Deployment | Variable parameterization for AE columns, new publish property IsAlwaysEncryptedParameterizationEnabled |
| Deployment | Support for IgnoreWorkloadClassifiers & IgnoreDatabaseWorkloadGroups publish properties |
| Deployment | Support for external language runtimes |
| ScriptDOM | Support for ledger database and tables |
| ScriptDOM | Support for INCLUDE columns in inline index definitions |

### Fixes
| Feature | Details |
| :------ | :------ |
| Deployment | Fixed an issue where external user deployment to Azure SQL Managed Instance would fail |
| Deployment | Fix for deployment order involving temporal tables to drop dependencies before turning system versioning off |
| Deployment | Fix for Always Encrypted deployment bug with error "Invalid object name '#tmpErrors'"  |
| Export | Validation for SqlPackage parameters ExcludeObjectType(s) and DoNotDropObjectType(s) |
| Export | Fixed export failure when there are change data capture (CDC) objects in database by excluding |
| Extract | Adds a retry to extract validation when first time fails due to race condition |
| Import | Fixed occasional deadlocks when importing to Azure by setting MAXDOP to 1 |
| Import | Fixed import failure when temporal table has dependency on security policy with schema binding on |
| Platform | DacFramework.msi is now signed by "Microsoft SQL Server Data-Tier Application Framework" instead of "SQL Server 2012" |
| Platform | Default to large arrays in x64 SqlPackage, fixes some scenarios involving large databases |
| Schema Compare | Fix for schema compare failing for equal databases with database scoped configurations |
| Schema Compare | Fixed schema compare with columnstore indexes |
| SQL Project | Fixed a bug with build error for "GRANT EXECUTE ANY EXTERNAL SCRIPT" |
| SQL Project | Fixed a bug where database project with columnstore index and a (n)varchar(max) column builds successfully but fails at deployment |
| SQL Project | Fixed unresolved reference warnings for table distribution columns within Stored Procedures |


### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported | N/A |
| Deployment | The Azure SQL ledger table feature isn't yet supported | N/A |

## 18.7.1 SqlPackage

**Release date:** June 2, 2021

**Build:** 15.0.5164.1

### Features
| Feature | Details |
| :------ | :------ |
| Auditing | Adds support for [EXTERNAL_MONITOR](/azure/azure-sql/managed-instance/auditing-configure). |
| Azure Synapse Analytics | Adds support for [PREDICT](../../t-sql/queries/predict-transact-sql.md). |
| Logging | Adds SqlPackage version and architecture information to diagnostic log file. |

### Fixes
| Feature | Details |
| :------ | :------ | 
| Export | Fixed an issue where exporting a table with text or image in the first column would fail without a clustered index. |
| Export | Fixed an issue where exporting a table  without a clustered index that has the order of columns in a statistic in a different order than the table create script would fail. |

## 18.7 SqlPackage

**Release date:** March 10, 2021

**Build:** 15.0.5084.2

### Features
| Feature | Details |
| :------ | :------ |
| Deployment | Extract/Publish Big Data to/from Azure Storage. For more info, see [SqlPackage for Big Data](SqlPackage-for-azure-synapse-analytics.md) |
| Azure Synapse Analytics | Row level security support (inline table-valued function, security policy, security predicate)  |
| Azure Synapse Analytics | Workload classification support |
| Azure SQL Edge | External streaming job support |
| Azure SQL Edge | Added table and database options for data retention. |
| Import | Added 2 new index option properties for import operation. *DisableIndexesForDataPhase* (Disable indexes before importing data into SQL Server, default true) and *RebuildIndexesOfflineForDataPhase* (Rebuild indexes offline after importing data into SQL Server, default false) |
| Logging | Added property for all operations (HashObjectNamesInLogs) that will turn all object names into a hash string in log messages. |
| Performance | Improvements to import and export performance, including additional logging to assist in determining additional bottlenecks. |
| SQLCMD | Added property for Deployment and Schema Compare (DoNotEvaluateSqlCmdVariables) that specifies whether SQLCMD variables will be replaced with values. |



### Fixes
| Feature | Details |
| :------ | :------ | 
| Deployment | Default MAXDOP changed from 0 to 8 for [Azure SQL](https://techcommunity.microsoft.com/t5/azure-sql/changing-default-maxdop-in-azure-sql-database/ba-p/1538528), updating schema model default in DacFx | 
| Schema Compare | Stored procedures using OUT and OUTPUT keywords to be ignored as a difference |
| Deployment | Additional validation for Big Data tokens |
| Build/Deployment | Full schema model cleanup of temp external tables for final dacpac consistency.  |
| Build/Deployment | Adding error handling and fixing non-Edge 150 RE. |
| Import/Deployment | Sequence value restored during deployment |
| Deployment | Fixed an issue where changing the compression option on clustered index caused the table to be recreated instead of alter index. |
| Deployment | Fixed an issue where a clustered columnstore index was dropped and recreated if table column changed. |
| Deployment | Fixed external users getting dropped and recreated during deployment. |
| Schema Compare | Fixed schema compare issue with external streaming job. |
| Import | Null reference exception raised when enabling ambient setting ReliableDdlEnabled scripting a deployment report.|
| Deployment | Fixed an issue where deployment steps containing system versioning would be created in the incorrect order. |
| Deployment | Fixed an issue where schema compare update or dacpac deploy failed due to target containing temporal tables. |
| Deployment | Reseeds identity value after deployment based on target's previous last value. |

### Known Issues
| Feature | Details | Workaround |
| :------ | :------ |:------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported | N/A |
| Deployment | In an incremental deploy scenario, when the user is dropping a temporal table along with dropping objects that are dependent on it, like functions, stored procedures etc. the deployment can fail. The script generation order tries to turn off SYSTEM_VERSIONING on the table that is a pre-req for dropping the table, but the order of generated steps is incorrect. [Work item](https://github.com/microsoft/azuredatastudio/issues/14655) | Generate the deployment script, move the System_Versioning OFF step to just before the table being dropped and then run the script. |

## 18.6 SqlPackage

**Release date:** September 18, 2020

**Build:** 15.0.4897.1

### Features
| Feature | Details |
| :------ | :------ |
| Platform | Updated SqlPackage for .NET Core version to .NET Core 3.1 |
| Always Encrypted | Added support for secure enclave import and export for SQL Server 2019 |
| Deployment | Added support to ignore change data capture enabled tables when exporting from Azure SQL Database |
| Deployment | Added support for index option OPTIMIZE_FOR_SEQUENTIAL_KEY in Azure SQL Database |
| Deployment | Added support for identity columns for Azure Synapse Analytics | 
| Help | Output the SqlPackage version in the help (/?) and support the /version parameter | 

### Fixes
| Feature | Details |
| :------ | :------ | 
| Deployment | Fixed an incorrect deployment script generated when targeting Azure SQL Managed Instance as a non-sysadmin user  | 
| Deployment | Fixed loading deployment contributors when running script actions | 
| Help | Output correct elapsed time in SqlPackage when operation take longer than 1 day | 
| Deployment | Fixed dacpac registration when deploying for .NET Core | 
| Deployment | Fixed SqlPackage on .NET Core handling of the /accessToken (/at) parameter | 
| Deployment | Allow ALTER TABLE statements in stored procedures as non-top level statements | 
| Deployment | Fixed Azure Synapse Analytics validation of materialized views to be case insensitive | 

### Known Issues
| Feature | Details |
| :------ | :------ |
| Deployment | The Azure Synapse Analytics Workload Management feature (Workload Groups and Workload Classifiers) isn't yet supported | 

## 18.5.1 SqlPackage

**Release date:** June 24, 2020

**Build:** 15.0.4826.1


### Fixes
| Feature | Details |
| :------ | :------ |
| Deployment | Fixed a regression that was introduced in 18.5 causing there to be an "Incorrect syntax near 'type'" error when deploying a dacpac or importing a bacpac with a user with external login to on premises | 

## 18.5 SqlPackage

**Release date:** April 28, 2020

**Build:** 15.0.4769.1


### Features
| Feature | Details |
| :------ | :------ |
| Deployment | Data Sensitivity classification now supported for SQL Server 2008 and up, Azure SQL Database, and Azure Synapse Analytics |
| Deployment | Add Azure Synapse Analytics support for table constraints |
| Deployment | Add Azure Synapse Analytics support for ordered clustered column store index |
| Deployment | Add support for External Data Source (Oracle, Teradata, MongoDB/CosmosDB, ODBC, Big Data Cluster) and External Table for SQL Server 2019 Big Data Cluster |
| Deployment | Add SQL Database Edge Instance as supported edition |
| Deployment | Support Azure SQL Managed Instance server names of the form '\<server>.\<dnszone>.database.windows.net' |
| Deployment | Add support for copy command in Azure Synapse Analytics |
| Deployment | Add deployment option 'IgnoreTablePartitionOptions' during Publish to avoid table recreation when there is change in partition function on table for Azure Synapse Analytics |
| .NET Core | Add support for Microsoft.Data.SqlClient in .NET Core version of SqlPackage |

### Fixes
| Fix | Details |
| :-- | :------ |
| Deployment | Fix parsing json path as expression |
| Deployment | Fix generating GRANT statements for AlterAnyDatabaseScopedConfiguration and AlterAnySensitivityClassification permissions |
| Deployment | Fix External Script permission not being recognized |
| Deployment | Fix for inline property - the implicit addition of the property should not show in difference but explicit mention should show through script |
| Deployment | Resolved an issue where changing a Table referenced by a Materialized View (MV) causes Alter View statements to be generated. Alter View statements are not supported for MVs for Azure Synapse Analytics. |
| Deployment | Fix publish failing when adding column to a table with data for Azure Synapse Analytics |
| Deployment | Fix update script should move data to a new table when changing the distribution column type (data loss scenario) for Azure Synapse Analytics |
| ScriptDom | Fix ScriptDom bug where it couldn't recognize inline constraints defined after an inline index |
| ScriptDom | Fix ScriptDom SYSTEM_TIME missing closing parenthesis when in a batch statement |
| Always Encrypted | Fix #tmpErrors table failing to drop if SqlPackage reconnects and the temp table is already gone because the temporary table goes away when the connection dies |

### Known Issues
| Feature | Details |
| :------ | :------ |
| Deployment |  A regression was introduced in 18.5 causing there to be an "Incorrect syntax near 'type'" error when deploying a dacpac or importing a bacpac with a user with external login to on premises. Workaround is to use SqlPackage 18.4 and it will be fixed in the next SqlPackage release. | 
| .NET Core | Importing bacpacs with sensitivity classification fails with "Internal connection fatal error" because of this [known issue](https://github.com/dotnet/SqlClient/issues/559) in Microsoft.Data.SqlClient. This will be fixed in the next SqlPackage release. |

## 18.4.1 SqlPackage

**Release date:** December 13, 2019

**Build:** 15.0.4630.1


### Fixes
| Fix | Details |
| :-- | :------ |
| ScriptDom |  A ScriptDom parsing regression was introduced in 18.3.1 where 'RENAME' is incorrectly treated as a top-level token, cause parsing to fail.

### Known Issues 

| Feature | Details |
| :------ | :------ |
| Deployment |  A regression was introduced in 18.4.1 causing there to be an "Object reference not set to an instance of an object." error when deploying a dacpac or importing a bacpac with a user with external login. Workaround is to use SqlPackage 18.4 and it will be fixed in the next SqlPackage release. | 

## 18.4 SqlPackage

**Release date:** October 29, 2019

**Build:** 15.0.4573.2


### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Add support to deploy to Azure Synapse Analytics. | 
| Platform | SqlPackage .NET Core generally available for macOS, Linux, and Windows. | 
| Security | Remove SHA1 code signing. |
| Deployment | Add support for new Azure database editions: GeneralPurpose, BusinessCritical, Hyperscale |
| Deployment | Add Azure SQL Managed Instance support for Azure Active Directory user and groups. |
| Deployment | Support the /AccessToken parameter for SqlPackage on .NET Core. |

### Known Issues 

| Feature | Details |
| :------ | :------ |
| ScriptDom |  A ScriptDom parsing regression was introduced in 18.3.1 where 'RENAME' is incorrectly treated as a top-level token, cause parsing to fail. This will be fixed in the next SqlPackage release. | 

### Known Issues for .NET Core

| Feature | Details |
| :------ | :------ |
| Import |  For .bacpac files with compressed files over 4GB in size, you might need to use the .NET Core version of SqlPackage to perform the import.  This behavior is due to how .NET Core generates zip headers, which although valid, are not readable by the .NET Full Framework version of SqlPackage. | 
| Deployment | The parameter /p:Storage=File isn't supported. Only Memory is supported on .NET Core. | 
| Always Encrypted | SqlPackage .NET Core doesn't support Always Encrypted columns. | 
| Security | SqlPackage .NET Core doesn't support the /ua parameter for multi-factor authentication. | 
| Deployment | Older V2 dacpac and bacpac files that use json data serialization aren't supported. |

## 18.3.1 SqlPackage

**Release date:** September 13, 2019

**Build:** 15.0.4538.1


### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Add support to deploy to Azure Synapse Analytics (preview). | 
| Deployment | Add /p:DatabaseLockTimeout=(INT32 '60') parameter to SqlPackage. | 
| Deployment | Add /p:LongRunningCommandTimeout=(INT32) parameter to SqlPackage. |
| Export/Extract | Add /p:TempDirectoryForTableData=(STRING) parameter to SqlPackage. |
| Deployment | Allow deployment contributors to be loaded from additional locations. Deployment contributors will be loaded from the same directory as the target .dacpac being deployed, the Extensions directory relative to the SqlPackage binary, and the /p:AdditionalDeploymentContributorPaths=(STRING) parameter added to SqlPackage where additional directory locations can be specified. |
| Deployment | Add support for OPTIMIZE_FOR_SEQUENTIAL_KEY. |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Fix to ignore automatic indexes so that they are not dropped on deployment. | 
| Always Encrypted | Fix for handling Always Encrypted varchar columns. | 
| Build/Deployment | Fix to resolve the nodes() method for xml column sets.| 
| ScriptDom | Fix additional cases where the 'URL' string was interpreted as a top level token. | 
| Graph | Fix generated SQL for pseudo column references in constraints.  | 
| Export | Generate random passwords that meet complexity requirements. | 
| Deployment | Fix to honor command timeouts when retrieving constraints. | 
| .NET Core (preview) | Fix diagnostic logging to a file. | 
| .NET Core (preview) | Use streaming to export table data to support large tables. | 

## 18.2 SqlPackage

**Release date:** April 15, 2019

**Build:** 15.0.4384.2


### Features

| Feature | Details |
| :------ | :------ |
| Graph | Add graph table support for edge constraints and edge constraint clauses. |
| Deployment | Enabled model validation rule to support 32 columns for index keys for SQL Server 2016 and up. |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Fix reverse engineering a SQL Server 2016 RTM database due to an unsupported query hint being used. |
| Deployment | Fix deployment ordering of auto close alter statements to occur before create filegroup statements. |
| ScriptDom | Fix ScriptDom parsing regression where the 'URL' string was interpreted as a top level token. |
| Deployment | Fix a null reference exception when parsing an alter table add index statement. | 
| Schema Compare | Fixed schema compare for nullable persisted computed columns always showing as different.|

## 18.1 SqlPackage

**Release date:** February 1, 2019

**Build:** 15.0.4316.1

Preview release.

### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Added support for UTF8 collations. |
| Deployment | Enabled nonclustered columnstore indexes on an indexed view. |
| Platform | Moved to .NET Core 2.2. | 
| Schema Compare | Use memory backed storage for schema compare on .NET Core. |

### Fixes

| Fix | Details |
| :-- | :------ |
| Performance | Performance fix to use the legacy cardinality estimator for reverse engineering queries. | 
| Performance | Fixed a significant schema compare performance issue when generating a script. | 
| Schema Compare | Fixed the schema drift detection logic to ignore certain extended event (xevent) sessions. |
| Graph | Fixed import ordering for graph tables. | 
| Export | Fixed exporting external tables with object permissions. |

### Known issues

This release includes cross-platform preview builds of SqlPackage that target .NET Core 2.2. The SqlPackage can run on macOS and Linux.

| Known issue | Details |
| :---------- | :------ |
| Deployment | For .NET Core, build and deployment contributors aren't supported. | 
| Deployment | For .NET Core, older dacpac and bacpac files that use json data serialization aren't supported. | 
| Deployment | For .NET Core referenced dacpacs (for example master.dacpac) may not resolve due to issues with case-sensitive file systems. A workaround is to capitalize the name of the reference file (for example MASTER.BACPAC). |

## 18.0 SqlPackage

**Release date:** October 24, 2018

**Build:** 15.0.4200.1

### Features

| Feature | Details |
| :------ | :------ |
| Deployment | Added support for database compatibility level 150. | 
| Deployment | Added support for Azure SQL Managed Instances. | 
| Performance | Added MaxParallelism command-line parameter to specify the degree of parallelism for database operations. | 
| Security | Added AccessToken command-line parameter to specify an authentication token when connecting to SQL Server. | 
| Import | Added support to stream BLOB/CLOB data types for imports. | 
| Deployment | Added support for scalar UDF 'INLINE' option. | 
| Graph | Added support for graph table 'MERGE' syntax. |

### Fixes

| Fix | Details |
| :-- | :------ |
| Graph | Fixed unresolved pseudo-column for graph tables. |
| Deployment | Fixed creating a database with memory optimized file groups when memory optimized tables are used. |
| Deployment | Fixed including extended properties on external tables. |

## 17.8 SqlPackage

**Release date:** June 22, 2018

**Build:** 14.0.4079.2

### Features

| Feature | Details |
| :------ | :------ |
| Diagnostics | Improved error messages for connection failures, including the SqlClient exception message. |
| Deployment | Support index compression on single partition indexes for import/export. |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Fixed a reverse engineering issue for XML column sets with SQL 2017 and later. | 
| Deployment | Fixed an issue where scripting the database compatibility level 140 was ignored for Azure SQL Database. |

## 17.4.1 SqlPackage

**Release date:** January 25, 2018

**Build:** 14.0.3917.1

### Features

| Feature | Details |
| :------ | :------ |
| Import/Export | Added ThreadMaxStackSize command-line parameter to parse Transact-SQL with a large number of nested statements. |
| Deployment | Database catalog collation support. | 

### Fixes

| Fix | Details |
| :-- | :------ |
| Import | When importing an Azure SQL Database bacpac to an on-premises instance, fixed errors due to _Database master keys without password are not supported in this version of SQL Server_. |
| Graph | Fixed an unresolved pseudo column error for graph tables. |
| Schema Compare | Fixed SQL authentication to compare schemas. | 

## 17.4.0 SqlPackage

**Release date:** December 12, 2017

**Build:** 14.0.3881.1

### Features

| Feature | Details |
| :------ | :------ |
| Deployment |  Added support for _temporal retention policy_ on SQL 2017+ and Azure SQL Database. | 
| Diagnostics | Added /DiagnosticsFile:"C:\Temp\SqlPackage.log" command-line parameter to specify a file path to save diagnostic information. | 
| Diagnostics | Added /Diagnostics command-line parameter to log diagnostic information to the console. |

### Fixes

| Fix | Details |
| :-- | :------ |
| Deployment | Do not block when encountering a database compatibility level that isn't understood. Instead, the latest Azure SQL Database or on-premises platform will be assumed. |
| &nbsp; | &nbsp; |
