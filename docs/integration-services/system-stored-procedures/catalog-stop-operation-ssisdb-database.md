---
title: "catalog.stop_operation (SSISDB Database)"
description: "catalog.stop_operation (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.stop_operation (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Stops a validation or instance of execution in the [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog.  
  
## Syntax  
  
```sql  
catalog.stop_operation [ @operation_id = ] operation_id  
```  
  
## Arguments  
 [ @operation_id = ] *operation_id*  
 The unique identifier of the validation or instance of execution. The *operation_id* is **bigint**.  
  
## Return Code Value  
 0 (success)  
  
## Result Sets  
 None  
  
## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   READ and MODIFY permissions on the validation or instance of execution  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role  
  
## Errors and Warnings  
 The following list describes some conditions that may raise an error or warning:  
  
-   The user does not have the appropriate permissions  
  
-   The operation identifier is not valid  
  
-   The operation has already been stopped  
  
## Remarks  
 Only one user at a time should stop an operation in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog. If multiple users try to stop the operation, the stored procedure will return success (the value `0`) on the first attempt, but subsequent attempts will raise an error.  
  
  
