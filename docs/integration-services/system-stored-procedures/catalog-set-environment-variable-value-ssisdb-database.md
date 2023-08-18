---
title: "catalog.set_environment_variable_value (SSISDB Database)"
description: "catalog.set_environment_variable_value (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.set_environment_variable_value (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Sets the value of an environment variable in the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog.  
  
## Syntax  
  
```sql  
catalog.set_environment_variable_value [ @folder_name = ] folder_name  
    , [ @environment_name = ] environment_name  
    , [ @variable_name = ] variable _name  
    , [ @value = ] value  
```  
  
## Arguments  
 [ @folder_name = ] *folder_name*  
 The name of the folder that contains the environment. The *folder_name* is **nvarchar(128)**.  
  
 [ @environment_name = ] *environment_name*  
 The name of the environment. The *environment_name* is **nvarchar(128)**.  
  
 [ @variable _name = ] *variable _name*  
 The name of the environment variable. The *variable _name* is **nvarchar(128)**.  
  
 [ @value = ] *value*  
 The value of the environment variable. The *value* is **sql_variant**.  
  
## Return Code Value  
 0 (success)  
  
## Result Sets  
 None  
  
## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   READ and MODIFY permissions on the environment  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
## Errors and Warnings  
 The following list describes some conditions that may raise an error or warning:  
  
-   The folder name is not valid  
  
-   The environment name is not valid  
  
-   The environment variable name is not valid  
  
-   The user does not have appropriate permissions  
  
  
