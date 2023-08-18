---
title: "Report Server Windows Service (MSSQLServer) 107"
description: "In this error reference page, learn about event ID 107: Report Server Windows Service (SQL Server) cannot connect to the report server database."
author: maggiesMSFT
ms.author: maggies
ms.date: 03/14/2017
ms.service: reporting-services
ms.subservice: troubleshooting
ms.topic: conceptual
ms.custom: updatefrequency5
helpviewer_keywords:
  - "MSSQLServer 107 error"
---
# Report Server Windows Service (MSSQLServer) 107
    
## Details  
  
|Category|Value|  
|-|-|  
|Product Name|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|Event ID|107|  
|Event Source|Report Server Windows Service|  
|Component|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|  
|Message Text|Report Server Windows Service (MSSQLSERVER) cannot connect to the report server database.|  
  
## Explanation  
 The [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Report Server service cannot connect to the report server database. This error occurs during a service restart if a connection to the report server database cannot be established. Conditions under which this error occurs include the following:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] service is not running when the Report Server service starts.  
  
-   The connection to the [!INCLUDE[ssDE](../../includes/ssde-md.md)] service fails because remote connections or the TCP/IP protocol is not enabled.  
  
-   The report server database is not configured correctly.  
  
-   The service account is not configured correctly, or the account no longer has permissions on the report server database. This can occur if you do not use the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool to set up the account or the report server database.  
  
## User Action  
 Start the [!INCLUDE[ssDE](../../includes/ssde-md.md)] service if it is not running and check that remote connections are enabled for TCP/IP protocol.  
  
 Use the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool to configure the report server database and service account.  
  
## Internal-Only  
  
## See Also  

 [Configure the Report Server Service Account &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md)   
 [Report Server Configuration Manager &#40;Native Mode&#41;](../../reporting-services/install-windows/reporting-services-configuration-manager-native-mode.md)   

 [Start and Stop the Report Server Service](../../reporting-services/report-server/start-and-stop-the-report-server-service.md)  
  
  
