---
title: Web Configuration Page
description: "Web Configuration Page (Master Data Services Configuration Manager)"
author: CordeliaGrey
ms.author: jiwang6
ms.date: "03/20/2017"
ms.service: sql
ms.subservice: master-data-services
ms.topic: conceptual
f1_keywords:
  - "sql13.mds.configmanager.webconfigpg.f1"
---
# Web Configuration Page (Master Data Services Configuration Manager)

[!INCLUDE [SQL Server - Windows only ASDBMI](../includes/applies-to-version/sql-windows-only-asdbmi.md)]

  Use the **Web Configuration** page to configure a website and web application. You can also enable Data Quality Services.  
  
## Configure the Web Application  
  
|Control Name|Description|  
|------------------|-----------------|  
|**Website**|Either create a new website, select the default website, or select another available site (if listed). This list displays the websites that are defined in Internet Information Services (IIS) on the local computer. When you create a new website, a new web application is automatically created. When you select the default or another existing site, you must create an application manually.|  
|**Web application**|Select a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] web application for configuration. This box shows the [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] web applications in the selected website only.<br /><br /> If nothing is displayed, click **Create** to create a website.|  
|**Create**|Opens the **Create Web Application** dialog box from which you create a [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] web application in the selected site. This button is enabled only when the selected site has no root web application configured as the [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] web application.|  
  
## Associate Application with Database  
  
|Control Name|Description|  
|------------------|-----------------|  
|**Select**|Opens the **Connect to Server** dialog box from which you connect to a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance and select a [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database to associate with the selected [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] web application.|  
|**SQL Server instance**|Displays the name of the selected [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance that hosts the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database. This is blank until you connect to a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance and select a database.|  
|**Database**|Displays the name of the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] database that is associated with the selected [!INCLUDE[ssMDSmdm](../includes/ssmdsmdm-md.md)] web application. This is blank until you connect to a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] instance and select a database.|  
  
## Enable DQS Integration  
  
|Control Name|Description|  
|------------------|-----------------|  
|**Enable integration with Data Quality Services**|Select this option to enable the Data Quality functionality available in the [!INCLUDE[ssMDSshort](../includes/ssmdsshort-md.md)] [!INCLUDE[ssMDSXLS](../includes/ssmdsxls-md.md)]. For more information, see [Enable Data Quality Services Integration with Master Data Services](../master-data-services/install-windows/enable-data-quality-services-integration-with-master-data-services.md).|  
  
## See Also  
[Master Data Services Installation and Configuration](../master-data-services/master-data-services-installation-and-configuration.md) 
 [Web Application Requirements &#40;Master Data Services&#41;](../master-data-services/install-windows/web-application-requirements-master-data-services.md)   
 [Create a Master Data Manager Web Application &#40;Master Data Services&#41;](../master-data-services/install-windows/create-a-master-data-manager-web-application-master-data-services.md)  
  
  
