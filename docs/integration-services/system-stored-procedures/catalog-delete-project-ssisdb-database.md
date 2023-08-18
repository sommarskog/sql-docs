---
title: "catalog.delete_project (SSISDB Database)"
description: "catalog.delete_project (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.delete_project (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Deletes an existing project from a folder in the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog.  
  
## Syntax  
  
```sql  
catalog.delete_project [ @folder_name = ] folder_name , [ @project_name = ] project_name  
```  
  
## Arguments  
 [ @folder_name = ] *folder_name*  
 The name of the folder that contains the project. *folder_name* is **nvarchar(128)**.  
  
 [ @project_name = ] *project_name*  
 The name of the project that is to be deleted. *project_name* is **nvarchar(128)**.  
  
## Return Code Value  
 0 (success)  
  
## Result Sets  
 None  
  
## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   READ and MODIFY permissions on the project  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
## Errors and Warnings  
 The following list describes some conditions that may cause the delete_project stored procedure to raise an error:  
  
-   The project does not exist  
  
-   The folder does not exist  
  
-   The user does not have the appropriate permissions  
  
## Remarks  
 All objects and environment references of the corresponding project are deleted along with the project. However, the versions of the project and the relevant operations records are retained until the next time the operation cleanup job runs.  
  
  
