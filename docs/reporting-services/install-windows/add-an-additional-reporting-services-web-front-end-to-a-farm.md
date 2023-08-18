---
title: "Add an Additional Reporting Services Web Front-end to a Farm"
description: "Add an Additional Reporting Services Web Front-end to a Farm"
author: maggiesMSFT
ms.author: maggies
ms.date: 05/30/2017
ms.service: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
monikerRange: ">=sql-server-2016 <=sql-server-2016"
---
# Add an Additional Reporting Services Web Front-end to a Farm
  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] SharePoint mode includes components needed for application servers and web front-end (WFE) servers. This topic focuses on installing the required [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] components for a WFE server, including the application pages used by [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] features such as subscriptions, data alerts, and Power View. The primary [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] installation needed for a WFE is to install the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] add-in for SharePoint 2016 products.  

> [!NOTE]
> Power View support is no longer available after SQL Server 2017.

## Prerequisites  
  
-   You must be a local administrator to run SQL Server Setup.  
  
-   The computer must be joined to a domain.  
  
-   You need to know the name of the existing database server that is hosting the SharePoint configuration and content databases.  
  
-   The database server must be configured to allow for remote database connections.  If it isn't, you won't be able to join the new server to the farm because the new server won't be able to make a connection to the SharePoint configuration databases.  
  
-   The new server will need to have the same version of SharePoint installed that the current farm servers are running. For example if the farm already has SharePoint 2013 Service Pack 1 (SP1) installed, you'll need to also install SP1 on the new server before it can join the farm.  
  
## Steps  
 The steps in this topic assume that a SharePoint farm administrator is installing and configuring the server. The diagram shows a typical three tier environment and the numbered items in the diagram are described in the following list:  
  
-   (1) Multiple web front-end (WFE) servers. The WFE servers require the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] add-in for SharePoint 2010. The following steps add a second application server to this tier.  
  
-   (2) Two application servers running [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] and web sites, for example Central Administration.  
  
-   (3) Two SQL Server database servers.  
  
-   (4) Represents a software or hardware network load balancing solution (NLB)  
  
 ![Add SSRS to a new SharePoint WFE](../../reporting-services/install-windows/media/rs-sharepointscale-wfe.gif "Add SSRS to a new SharePoint WFE")  
  
 The following steps assume that an administrator is installing and configuring the server.  
  
|Step|Description and Link|  
|----------|--------------------------|  
|Add a SharePoint server to a farm.|You'll need to install SharePoint to deploy another Reporting Services application.<br/><br/>For SharePoint 2013, see [Add SharePoint server to a farm in SharePoint Server 2013](/SharePoint/install/add-web-or-application-server-to-the-farm).<br/><br/>For SharePoint 2016, see [Add SharePoint server to a farm in SharePoint Server 2016](/SharePoint/install/add-a-server-to-a-sharepoint-server-2016-farm).|  
|Install the SQL Server Reporting Services add-in for SharePoint 2016 products.|There are several methods for installing the add-in. The following steps use the SQL Server setup wizard. For more information on installing the add-in, see [Install or Uninstall the Reporting Services Add-in for SharePoint](../../reporting-services/install-windows/install-or-uninstall-the-reporting-services-add-in-for-sharepoint.md)<br /><br /> 1) Run SQL Server installation.<br /><br /> 2) On the **Setup Role** page, select **SQL Server Feature Installation**<br /><br /> 3) On the **Feature Selection** page, select **Reporting Services add-in for SharePoint products**<br /><br /> 4) Click **Next** on the next several pages to complete the setup options.<br /><br/>For more information on installing [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], see [Install the first Report Server in SharePoint mode](install-the-first-report-server-in-sharepoint-mode.md)|  
|Verify the new server is operational.|1) In SharePoint Central Administration, click **Manage servers in this farm** in the **System Settings** group.<br /><br /> 2) Verify the new server is in the list.|  
|Update your NLB solution.|If appropriate, update your hardware or software NLB environment to include the new server.|  

## Next steps

[Add SharePoint server to a farm in SharePoint Server 2016](/SharePoint/install/add-a-server-to-a-sharepoint-server-2016-farm)  
[Add SharePoint server to a farm in SharePoint Server 2013](/SharePoint/install/add-web-or-application-server-to-the-farm)

More questions? [Try asking the Reporting Services forum](https://go.microsoft.com/fwlink/?LinkId=620231)
