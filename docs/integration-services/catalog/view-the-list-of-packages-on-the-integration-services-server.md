---
title: "View the List of Packages on the Integration Services Server"
description: "View the List of Packages on the Integration Services Server"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
---
# View the List of Packages on the Integration Services Server

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  You can view the list of packages that are stored on the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server in one of two ways.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 To view the list of packages that are stored on the server, query the view, [catalog.packages &#40;SSISDB Database&#41;](../../integration-services/system-views/catalog-packages-ssisdb-database.md).  
  
 In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
 To view packages stored on the server by using Object Explorer in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], follow the procedure below.  
  
### To view packages using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connect to the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server. That is, connect to the instance of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] that hosts the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] database.  
  
2.  In Object Explorer, expand the tree to display the **Integration Services Catalogs** node.  
  
3.  Expand the **Integration Services Catalogs** node to display the **SSISDB** node.  
  
4.  Expand the **SSISDB** node to display a list of one or more folders. Each folder contains one or more projects in the **Projects** folder, and each project contains one more packages in the **Packages** folder.  
  
  
