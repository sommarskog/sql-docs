---
title: "catalog.clear_object_parameter_value (SSISDB Database)"
description: "catalog.clear_object_parameter_value (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.clear_object_parameter_value (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Clears the value of a parameter for an existing [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] project or package that is stored on the server.  
  
## Syntax  
  
```sql  
catalog.clear_object_parameter [ @folder_name = ] folder_name   
    , [ @project_name = ] project_name   
    , [ @object_type = ] object_type   
    , [ @object_name = ] object_name   
    , [ @parameter_ name = ] parameter_name  
```  
  
## Arguments  
 [ \@folder_name = ] *folder_name*  
 The name of the folder that contains the project. The *folder_name* is **nvarchar(128)**.  
  
 [ \@project_name = ] *project_name*  
 The name of project. The *project_name* is **nvarchar(128)**.  
  
 [ \@object_type = ] *object_type*  
 The type of object. Valid values include `20` for a project and `30` for a package. The *object_type* is **smallInt**.  
  
 [ \@ object _name = ] *object _name*  
 The name of the package. The *object _name* is **nvarchar(260)**.  
  
 [ \@parameter_ name = ] *parameter_name*  
 The name of the parameter. The *parameter_ name* is **nvarchar(128)**.  
  
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
 The following list describes some conditions that may cause the clear_object_parameter stored procedure to raise an error:  
  
-   An invalid object type is specified or the object name cannot be found in the project.  
  
-   The project does not exist, the project is not accessible, or the project name is invalid  
  
-   An invalid parameter name is specified.  
  
-   The user does not have the appropriate permissions.  
  
  
