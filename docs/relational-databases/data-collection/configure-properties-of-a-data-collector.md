---
title: "Configure Properties of a Data Collector"
description: "Configure Properties of a Data Collector"
author: MashaMSFT
ms.author: mathoma
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: supportability
ms.topic: conceptual
f1_keywords:
  - "sql13.swb.dc.datacollectionprop.general.f1"
  - "sql13.swb.dc.datacollectionprop.advanced.f1"
---
# Configure Properties of a Data Collector
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  This topic discusses how you can configure the properties of a data collector.  
  
## Data Collection Properties (General Tab)  
 Use this page to configure settings for the management data warehouse and specify where collected data should be stored before it is uploaded to the data warehouse.  
  
 **Enable Data Collection**  
 Select to enable data collection. This has the same effect as running the sp_syscollector_enable_collector stored procedure. Clearing this check box disables data collection and has the same effect as running the sp_syscollector_disable_collector stored procedure.  
  
 **Server**  
 Displays the name of the server that will host the management data warehouse  
  
 **Database name**  
 Displays the name of the relational database that is used for the management data warehouse.  
  
 **Test Connection**  
 Test the connection to the specified **Server** using information provided when data collection is configured.  
  
 **Cache directory**  
 Specifies the directory where collected data is stored on the system collecting the data before it is uploaded to the management data warehouse. If **Cache directory** is not specified, the data collector attempts to locate the %TEMP% and %TMP% environment variables and use one these locations as the default location for temporary storage. If these environment variables are not configured, an error occurs and you are prompted to create a cache directory.  
  
## Data Collection Properties (Advanced Tab)  
 Use this page to configure the retry settings for the connection to the management data warehouse.  
  
 **Number of times to retry if upload fails**  
 Specifies the number of times to retry an upload to the management data warehouse if an upload fails. The default is 1.  
  
## See Also  
 [Manage Data Collection](../../relational-databases/data-collection/manage-data-collection.md)   
 [Configure the Management Data Warehouse &#40;SQL Server Management Studio&#41;](../../relational-databases/data-collection/configure-the-management-data-warehouse-sql-server-management-studio.md)  
  
  
