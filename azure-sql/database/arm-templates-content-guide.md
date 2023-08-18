---
title: Azure Resource Manager templates
description: Use Azure Resource Manager templates to create and configure Azure SQL Database and Azure SQL Managed Instance.
author: urosmil
ms.author: urmilano
ms.reviewer: wiassaf, mathoma
ms.date: 06/30/2021
ms.service: sql-db-mi
ms.subservice: deployment-configuration
ms.topic: conceptual
ms.custom: overview-samples sqldbrb=2, devx-track-arm-template
---

# Azure Resource Manager templates for Azure SQL Database & SQL Managed Instance
[!INCLUDE[appliesto-sqldb-sqlmi](../includes/appliesto-sqldb-sqlmi.md)]

Azure Resource Manager templates enable you to define your infrastructure as code and deploy your solutions to the Azure cloud for Azure SQL Database and Azure SQL Managed Instance.

## [Azure SQL Database](#tab/single-database)

The following table includes links to Azure Resource Manager templates for Azure SQL Database.

|Link |Description|
|---|---|
| [SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-database-transparent-encryption-create) | This Azure Resource Manager template creates a single database in Azure SQL Database and configures server-level IP firewall rules. |
| [Server](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-logical-server) | This Azure Resource Manager template creates a server for Azure SQL Database. |
| [Elastic pool](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-elastic-pool-create) | This template allows you to deploy an elastic pool and to assign databases to it. |
| [Failover groups](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-with-failover-group) | This template creates two servers, a single database, and a failover group in Azure SQL Database.|
| [Auditing to Azure Blob storage](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-auditing-server-policy-to-blob-storage) | This template allows you to deploy a server with auditing enabled to write audit logs to a Blob storage. Auditing for Azure SQL Database tracks database events and writes them to an audit log that can be placed in your Azure storage account, OMS workspace, or Event Hubs.|
| [Auditing to Azure Event Hub](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-auditing-server-policy-to-eventhub) | This template allows you to deploy a server with auditing enabled to write audit logs to an existing event hub. In order to send audit events to Event Hubs, set auditing settings with `Enabled` `State`, and set `IsAzureMonitorTargetEnabled` as `true`. Also, configure Diagnostic Settings with the `SQLSecurityAuditEvents` log category on the `master` database (for server-level auditing). Auditing tracks database events and writes them to an audit log that can be placed in your Azure storage account, OMS workspace, or Event Hubs.|
| [Azure Web App with SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/web-app-sql-database) | This sample creates a free Azure web app and a database in Azure SQL Database at the "Basic" service level.|
| [Azure Web App and Redis Cache with SQL Database](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/web-app-redis-cache-sql-database) | This template creates a web app, Redis Cache, and database in the same resource group and creates two connection strings in the web app for the database and Redis Cache.|
| [Import data from Blob storage using ADF V2](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.datafactory/data-factory-v2-blob-to-sql-copy) | This Azure Resource Manager template creates an instance of Azure Data Factory V2 that copies data from Azure Blob storage to SQL Database.|
| [HDInsight cluster with a database](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.hdinsight/hdinsight-linux-with-sql-database) | This template allows you to create an HDInsight cluster, a logical SQL server, a database, and two tables. This template is used by the [Use Sqoop with Hadoop in HDInsight article](/azure/hdinsight/hadoop/hdinsight-use-sqoop). |
| [Azure Logic App that runs a SQL Stored Procedure on a schedule](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.logic/logic-app-sql-proc) | This template allows you to create a logic app that will run a SQL stored procedure on schedule. Any arguments for the procedure can be put into the body section of the template.|
| [Provision server with Azure AD-only authentication enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-logical-server-aad-only-auth) | This template creates a SQL logical server with an Azure AD admin set for the server and Azure AD-only authentication enabled. |

## [Azure SQL Managed Instance](#tab/managed-instance)

The following table includes links to Azure Resource Manager templates for Azure SQL Managed Instance.

|Link|Description|
|---|---|
| [SQL Managed Instance in a new VNet](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sqlmi-new-vnet) | This Azure Resource Manager template creates a new configured Azure virtual network and managed instance in the virtual network. |
| [Network environment for SQL Managed Instance](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sql-managed-instance-azure-environment) | This deployment will create a configured Azure virtual network with two subnets, one that will be dedicated to your managed instances and another where you can place other resources (for example VMs, App Service environments, etc.). This template will create a properly configured networking environment where you can deploy managed instances. |
| [SQL Managed Instance with P2S connection](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sqlmi-new-vnet-w-point-to-site-vpn) | This deployment will create an Azure virtual network with two subnets, `ManagedInstance` and `GatewaySubnet`. SQL Managed Instance will be deployed in the ManagedInstance subnet. A virtual network gateway will be created in the `GatewaySubnet` subnet and configured for Point-to-Site VPN connection. |
| [SQL Managed Instance with a virtual machine](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sqlmi-new-vnet-w-jumpbox) | This deployment will create an Azure virtual network with two subnets, `ManagedInstance` and `Management`. SQL Managed Instance will be deployed in the `ManagedInstance` subnet. A virtual machine with the latest version of SQL Server Management Studio (SSMS) will be deployed in the `Management` subnet. |
| [SQL Managed Instance with diagnostic logs enabled](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.sql/sqlmi-new-vnet-w-diagnostic-settings) | This deployment creates an Azure Virtual Network with `ManagedInstance` subnet and deploys a Managed Instance inside with enabled diagnostic logs. It will also deploy event hub, diagnostic workspace and storage account for the purpose of sending and storing instance diagnostic logs. |

---
