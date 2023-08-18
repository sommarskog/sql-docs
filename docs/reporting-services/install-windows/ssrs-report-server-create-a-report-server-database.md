---
title: "Create a report server database, Configuration Manager"
description: "SQL Server Reporting Services native mode uses two SQL Server relational databases to store report server metadata and objects. One database is used for primary storage, and the second one stores temporary data."
author: maggiesMSFT
ms.author: maggies
ms.date: 02/13/2023
ms.service: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
---

# Create a report server database, Report Server Configuration Manager  

[!INCLUDE [ssrs-appliesto](../../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016-and-later](../../includes/ssrs-appliesto-2016-and-later.md)] [!INCLUDE[ssrs-appliesto-pbirsi](../../includes/ssrs-appliesto-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

[!INCLUDE [ssrs-previous-versions](../../includes/ssrs-previous-versions.md)]

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] native mode uses two [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] relational databases to store report server metadata and objects. One database is used for primary storage, and the second one stores temporary data. 

The databases are created together and bound by name. With a default [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance, the databases are named **reportserver** and **reportservertempdb**. Collectively, the two databases are called the **report server database** or **report server catalog**.

::: moniker range="=sql-server-2016"

SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] **SharePoint mode** includes a third database that's used for data alerting metadata. The three databases are created for each SSRS service application. The database names by default include a GUID that represents the service application. 

The following are example names of the three SharePoint mode databases:

- ReportingService_90a9f37075544f22953c4a62e4a9f370  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370TempDB  
  
- ReportingService_90a9f37075544f22953c4a62e4a9f370_Alerting  

::: moniker-end
  
> [!IMPORTANT]  
> Don't write applications that run queries against the report server database. The report server database isn't a public schema. The table structure might change from one release to the next. If you write an application that requires access to the report server database, always use the SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] APIs to access the report server database.  
>
> Execution log views are exceptions to this rule. For more information, see [Report Server ExecutionLog and the ExecutionLog3 View](../../reporting-services/report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
## Ways to create the report server database

 ### Native mode
 You can create the native mode report server database in the following ways:  
  
- **Automatic**. Use the SQL Server setup wizard if you choose the default configuration option for installation. In the SQL Server Installation Wizard, this option is **Install and configure** on the **Report Server Installation Options** page. If you choose the **Install only** option, you must use SQL Server Report Server Configuration Manager to create the database. (Applies only to SQL Server Reporting Services 2016 and earlier)
  
- **Manual**. Use SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration Manager. Create the report server database manually if you use a remote [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] to host the database. For more information, see [Create a Native Mode Report Server Database](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  

::: moniker range="=sql-server-2016"
  
### SharePoint mode 
The **Report Server Installation Options** page has only one option for SharePoint mode, **Install Only**. This option installs all the SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] files and the SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] shared service. The next step is to create at least one SSRS service application in one of the following ways:  
  
- Go to Central Administration in SharePoint Server to create an SSRS service application. For more information, see the **create a service application** section of [Install the first Report Server in SharePoint mode](../../reporting-services/install-windows/install-the-first-report-server-in-sharepoint-mode.md#bkmk_create_serrviceapplication).  
  
- Use SQL Server [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] PowerShell cmdlets to create a service application and the report server databases. For more information, see the sample for creating service applications in the topic [PowerShell cmdlets for Reporting Services SharePoint mode](../../reporting-services/report-server-sharepoint/powershell-cmdlets-for-reporting-services-sharepoint-mode.md).  

::: moniker-end
  
## Database server version requirements

 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is used to host the report server databases. The [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] instance can be local or remote. The following supported versions of [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] can host the report server databases:  
::: moniker range=">=sql-server-ver15"

- Azure SQL Managed Instance

- SQL Server 2022

- SQL Server 2019

::: moniker-end
::: moniker range=">=sql-server-2017"

- SQL Server 2017  
::: moniker-end

- [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]  
  
- [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]  
  
- [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]  

> [!NOTE] 
> SQL on Linux isn't a supported environment to host a SQL Server Reporting Services database.

If you create the report server database on a remote computer, configure the connection to use a domain user account or a service account that has network access. If you use a remote [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance, consider which credentials the report server should use to connect to the instance. For more information, see [Configure a Report Server Database Connection &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-report-server-database-connection-ssrs-configuration-manager.md).  
  
> [!IMPORTANT]  
> The report server and the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance hosting the report server database can be in different domains. For internet deployment, it's common practice to use a server that's behind a firewall. 
>
> If you configure a report server for internet access, use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] credentials to connect to the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] that's behind the firewall. Secure the connection by using IPSEC.  
  
## Edition requirements for a database server 

 When you create a report server database, not all editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can be used to host the database. For more information, see [Edition requirements for the report server database](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md#edition-requirements-for-the-report-server-database) in [SQL Server Reporting Services features supported by its editions](../reporting-services-features-supported-by-the-editions-of-sql-server-2016.md).  

## Next steps

Read about [Report Server Configuration Manager](reporting-services-configuration-manager-native-mode.md).  

More questions? Ask the [Reporting Services forum](/answers/search.html?c=&f=&includeChildren=&q=ssrs+OR+reporting+services&redirect=search%2fsearch&sort=relevance&type=question+OR+idea+OR+kbentry+OR+answer+OR+topic+OR+user).
