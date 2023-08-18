---
title: "Copy a Package in SQL Server Data Tools"
description: "Copy a Package in SQL Server Data Tools"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
helpviewer_keywords:
  - "packages [Integration Services], copying"
  - "copying packages"
  - "regenerating package GUID"
  - "updating package properties"
---
# Copy a Package in SQL Server Data Tools

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]


  This topic describes how to create a new [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] package by copying an existing package, and how to update the **Name** and **GUID** properties of the new package.  
  
### To copy a package  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], open the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] project that contains the package that you want to copy.  
  
2.  In Solution Explorer, double-click the package.  
  
3.  Verify either the package to copy is selected in Solution Explorer or the tab in SSIS Designer that contains the package is the active tab  
  
4.  On the **File** menu, click **Save \<package name> As**.  
  
    > [!NOTE]  
    >  The package must be opened in SSIS Designer before the **Save As** option appears on the **File** menu.  
  
5.  Optionally, browse to a different folder.  
  
6.  Update the name of the package file. Make sure that you retain the .dtsx file extension.  
  
7.  Click **Save**.  
  
8.  At the prompt, choose whether to update the name of the package object to match the file name. If you click **Yes**, the **Name** property of the package is updated. The new package is added to the [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] project and opened in [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer.  
  
9. Optionally, click in the background of the **Control Flow** tab, and the click **Properties**.  
  
10. In the Properties window, click the value of the ID property, and then in the drop-down list click **\<Generate New ID>**.  
  
11. On the **File** menu, click **Save Selected Items** to save the new package.  
  
## See Also  
 [Save a Copy of a Package](./save-packages.md)   
 [Create Packages in SQL Server Data Tools](../integration-services/create-packages-in-sql-server-data-tools.md)   
 [Integration Services &#40;SSIS&#41; Packages](../integration-services/integration-services-ssis-packages.md)  
  
