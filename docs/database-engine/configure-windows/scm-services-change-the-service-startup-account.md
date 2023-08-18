---
title: "SCM Services - Change the Service Startup Account"
description: Learn how to change the service accounts that SQL Server and many of its services use. View limitations and restrictions on changes in service accounts.
author: rwestMSFT
ms.author: randolphwest
ms.date: "01/06/2016"
ms.service: sql
ms.subservice: configuration
ms.topic: conceptual
helpviewer_keywords:
  - "SQL Server services, startup account changes"
  - "startup accounts [SQL Server]"
  - "changing startup accounts for services"
---
# SCM Services - Change the Service Startup Account
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic describes how to use [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager to change the start up options of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] services and to change the service accounts that are used by the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], and [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] with [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)], or PowerShell. For more information about how to select an appropriate service account, see [Configure Windows Service Accounts and Permissions](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
> [!IMPORTANT]  
>  When you change the service startup account for the [!INCLUDE[ssDE](../../includes/ssde-md.md)] and [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service (the [!INCLUDE[ssDE](../../includes/ssde-md.md)]) must be restarted for the change to take effect. When the service is restarted, all databases associated with that instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will be unavailable until the service successfully restarts. If you have to change the service startup account of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, make sure that you do so during regularly scheduled maintenance or when the databases can be taken offline without interrupting daily operations.  
  
##  <a name="BeforeYouBegin"></a> Before You Begin  
  
###  <a name="Restrictions"></a> Limitations and Restrictions  
  
-   Clustered servers  
  
     Changing the service account that is used by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent must be performed from the active node of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cluster.  
  
     When running on Windows Server 2008 (in a non-default configuration using Domain groups), changing the service account that is used by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent requires [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager to stop [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] by taking the resource groups offline.  
  
-   SKU Upgrade ([!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] to non-Express SKU)  
  
     During [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] installation, the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service is configured to use the Network Service account but disabled. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager can change the account assigned for the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service   but the service cannot be enabled or started. After SKU upgrade from [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] to non-Express, the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent service is not automatically enabled, but can be enabled when needed by using the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager and changing the service start mode to Manual or Automatic.  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Configuration Manager  
  
#### To change the SQL Server service startup account  
  
1.  On the **Start** menu, point to **All Programs**, point to **[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]**, point to **Configuration Tools**, and then click **[!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] Configuration Manager**.  
  
    > [!NOTE]  
    >  Because [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager is a snap-in for the [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console program and not a stand-alone program, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager does not appear as an application in newer versions of Windows.  
    >   
    >  -   **Windows 10 and Windows 11**:  
    >          To open [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, on the **Start Page**, type SQLServerManager13.msc (for [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]). For other versions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] replace 13 with the appropriate number. Clicking SQLServerManager13.msc opens the Configuration Manager. To pin the Configuration Manager to the Start Page or Task Bar, right-click SQLServerManager13.msc, and then click **Open file location**. In the Windows File Explorer, right-click SQLServerManager13.msc, and then click **Pin to Start** or **Pin to taskbar**.  
    > -   **Windows 8**:  
    >          To open [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, in the **Search** charm, under **Apps**, type **SQLServerManager\<version>.msc** such as **SQLServerManager13.msc**, and then press **Enter**.  
  
2.  In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, click **SQL Server Services**.  
  
3.  In the details pane, right-click the name of the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance for which you want to change the service startup account, and then click **Properties**.  
  
4.  In the **SQL Server \<**_instancename_**> Properties** dialog box, click the **Log On** tab, and select a **Log on as** account type.  
  
5.  After selecting the new service startup account, click **OK**.  
  
     A message box asks whether you want to restart the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] service.  
  
6.  Click **Yes**, and then close [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager.  
  
## See Also  
 [Start, Stop, Pause, Resume, Restart the Database Engine, SQL Server Agent, or SQL Server Browser Service](../../database-engine/configure-windows/start-stop-pause-resume-restart-sql-server-services.md)   
 [Configure WMI to Show Server Status in SQL Server Tools](../../ssms/configure-wmi-to-show-server-status-in-sql-server-tools.md)  
  
  
