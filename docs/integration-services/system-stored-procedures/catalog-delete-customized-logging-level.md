---
title: "catalog.delete_customized_logging_level"
description: "catalog.delete_customized_logging_level"
author: chugugrace
ms.author: chugu
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: "language-reference"
---
# catalog.delete_customized_logging_level 

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  Deletes an existing customized logging level. For more info about customized logging levels, see [Integration Services &#40;SSIS&#41; Logging](../../integration-services/performance/integration-services-ssis-logging.md).  
  
## Syntax  
  
```sql  
catalog.delete_customized_logging_level [ @level_name = ] level_name
```  
  
## Arguments  
 [ @level_name = ] *level_name*  
 The name of the existing customized logging level to delete.  
  
 The *level_name* is **nvarchar(128)**.  
  
## Remarks  
  
## Return Codes  
 0 (success)  
  
 When the stored procedure fails, it throws an error.  
  
## Result Set  
 None  
  
## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   Membership in the **ssis_admin** database role  
  
-   Membership in the **sysadmin** server role  
  
## Errors and Warnings  
 The following list describes conditions that cause the stored procedure to fail.  
  
-   The user does not have the required permissions.  
  
  
