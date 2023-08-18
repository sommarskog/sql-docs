---
title: "Browse All Principals Dialog Box"
description: "Browse All Principals Dialog Box"
author: chugugrace
ms.author: chugu
ms.date: "03/01/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
f1_keywords:
  - "sql13.ssis.ssms.browseprincipals.f1"
---
# Browse All Principals Dialog Box

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Use the **Browse All Principals** dialog box to select a database principal to change the principal's permissions on the selected project or on all projects contained in a selected folder.  
  
 **What do you want to do?**  
  
-   [Open the Browse All Principals dialog box](#open_dialog)  
  
-   [Configure the Options](#options)  
  
##  <a name="open_dialog"></a> Open the Browse All Principals dialog box  
  
1.  In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], connect to the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] server.  
  
     You're connecting to the instance of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] that hosts the SSISDB catalog.  
  
2.  In Object Explorer, expand the tree to display the **Integration Services Catalogs** node.  
  
3.  Expand the **SSISDB** node.  
  
4.  To change the principal's permissions on all projects contained in a selected folder, right-click the folder and then click **Properties**.  
  
     To change the principal's permissions on a selected project, expand the folder that contains the project, right-click the project, and then click **Properties**.  
  
5.  Select the **Permissions** page, and then click **Browse**.  
  
##  <a name="options"></a> Configure the Options  
 This page displays the principals from the catalog view, sys.database_principals, of the SSISDB database.  
  
 Selecting principals adds them to the **Logins or roles** list on the **Permissions** page of the parent dialog box when you click **OK** and close the **Browse All Principals** dialog box. After adding principals to the **Logins or roles** list, you can change their permissions on the selected project.  
  
 **Selection column**  
 Select to add the principal to the **Logins or roles** list on the **Permissions** page of the parent dialog box.  
  
 **Icon column**  
 An icon that corresponds to the **Type** of the principal.  
  
 **Name**  
 The name of the principal.  
  
 **Type**  
 The type of the principal. The common types are:  
  
-   SQL User  
  
-   Windows User  
  
-   Database Role  
  
  
