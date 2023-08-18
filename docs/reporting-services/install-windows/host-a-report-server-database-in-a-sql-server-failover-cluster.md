---
title: "Host a Report Server Database in a SQL Server Failover Cluster"
description: "Host a Report Server Database in a SQL Server Failover Cluster"
author: maggiesMSFT
ms.author: maggies
ms.date: 03/30/2016
ms.service: reporting-services
ms.topic: conceptual
ms.custom: updatefrequency5
---
# Host a Report Server Database in a SQL Server Failover Cluster
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provides failover clustering support so that you can use multiple disks for one or more [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instances. Failover clustering is supported only for the report server database; you cannot run the Report Server service as part of a failover cluster.  
  
 To host a report server database on a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover cluster, the cluster must already be installed and configured. You can then select the failover cluster as the server name when you create the report server database in the Database Setup page of the [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Configuration tool.  
  
 Although the Report Server service cannot participate in a failover cluster, you can install [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] on a computer that has a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover cluster installed. The report server runs independently of the failover cluster. If you install a report server on a computer that is part of a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] failover instance, you are not required to use the failover cluster for the report server database; you can use a different [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instance to host the database.  
  
## See Also  
 [Report Server Database &#40;SSRS Native Mode&#41;](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
 [Create a Report Server Database  &#40;Report Server Configuration Manager&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-report-server-database.md)  
  
  
