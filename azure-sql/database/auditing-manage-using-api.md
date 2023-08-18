---
title: Manage Azure SQL Database Auditing using APIs
description: Use Azure SQL Database auditing to track database events into an audit log.
author: sravanisaluru
ms.author: srsaluru
ms.date: 04/26/2023
ms.service: sql-database
ms.subservice: security
ms.custom: devx-track-azurepowershell
ms.topic: conceptual
---
# Manage Azure SQL Database Auditing using APIs

[!INCLUDE[appliesto-sqldb-asa](../includes/appliesto-sqldb-asa.md)]

This article provides an overview of the different APIs used for managing Auditing for Azure SQL Database and Azure Synapse Analytics.

## Use Azure PowerShell

**PowerShell cmdlets (including WHERE clause support for additional filtering)**:

- [Create or Update Database Auditing Policy (Set-AzSqlDatabaseAudit)](/powershell/module/az.sql/set-azsqldatabaseaudit)
- [Create or Update Server Auditing Policy (Set-AzSqlServerAudit)](/powershell/module/az.sql/set-azsqlserveraudit)
- [Get Database Auditing Policy (Get-AzSqlDatabaseAudit)](/powershell/module/az.sql/get-azsqldatabaseaudit)
- [Get Server Auditing Policy (Get-AzSqlServerAudit)](/powershell/module/az.sql/get-azsqlserveraudit)
- [Remove Database Auditing Policy (Remove-AzSqlDatabaseAudit)](/powershell/module/az.sql/remove-azsqldatabaseaudit)
- [Remove Server Auditing Policy (Remove-AzSqlServerAudit)](/powershell/module/az.sql/remove-azsqlserveraudit)

For a script example, see [Configure auditing and threat detection using PowerShell](scripts/auditing-threat-detection-powershell-configure.md).

### Use REST API

**REST API**:

- [Create or Update Database Auditing Policy](/rest/api/sql/2017-03-01-preview/database-auditing-settings/create-or-update)
- [Create or Update Server Auditing Policy](/rest/api/sql/2017-03-01-preview/server-auditing-settings/create-or-update)
- [Get Database Auditing Policy](/rest/api/sql/2017-03-01-preview/database-auditing-settings/get)
- [Get Server Auditing Policy](/rest/api/sql/2017-03-01-preview/server-auditing-settings/get)

Extended policy with WHERE clause support for additional filtering:

- [Create or Update Database *Extended* Auditing Policy](/rest/api/sql/2017-03-01-preview/database-extended-auditing-settings/create-or-update)
- [Create or Update Server *Extended* Auditing Policy](/rest/api/sql/server%20auditing%20settings/createorupdate)
- [Get Database *Extended* Auditing Policy](/rest/api/sql/2017-03-01-preview/database-extended-auditing-settings/get)
- [Get Server *Extended* Auditing Policy](/rest/api/sql/2017-03-01-preview/server-extended-auditing-settings/get)

### Use Azure CLI

- [Manage a server's auditing policy](/cli/azure/sql/server/audit-policy)
- [Manage a database's auditing policy](/cli/azure/sql/db/audit-policy)

### Use Azure Resource Manager templates

You can manage Azure SQL Database auditing using [Azure Resource Manager](/azure/azure-resource-manager/management/overview) templates, as shown in these examples:

- [Deploy an Azure SQL Database with Auditing enabled to write audit logs to Azure Blob storage account](https://azure.microsoft.com/resources/templates/sql-auditing-server-policy-to-blob-storage/)
- [Deploy an Azure SQL Database with Auditing enabled to write audit logs to Log Analytics](https://azure.microsoft.com/resources/templates/sql-auditing-server-policy-to-oms/)
- [Deploy an Azure SQL Database with Auditing enabled to write audit logs to Event Hubs](https://azure.microsoft.com/resources/templates/sql-auditing-server-policy-to-eventhub/)

> [!NOTE]  
> The linked samples are on an external public repository and are provided 'as is', without warranty, and are not supported under any Microsoft support program/service.

## See also

- [Auditing overview](auditing-overview.md)
- Data Exposed episode [What's New in Azure SQL Auditing](/Shows/Data-Exposed/Whats-New-in-Azure-SQL-Auditing)
- [Auditing for SQL Managed Instance](../managed-instance/auditing-configure.md)
- [Auditing for SQL Server](/sql/relational-databases/security/auditing/sql-server-audit-database-engine)
