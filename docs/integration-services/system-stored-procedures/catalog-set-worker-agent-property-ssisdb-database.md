---
title: "catalog.set_worker_agent_property (SSISDB Database)"
description: "catalog.set_worker_agent_property (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "03/02/2017"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
---
# catalog.set_worker_agent_property (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Sets the property of a [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out Worker.

## Syntax

```sql
catalog.set_worker_agent_property [ @WorkerAgentId = ] WorkerAgentId
    , [ @PropertyName = ] PropertyName
    , [ @PropertyValue = ] PropertyValue 
```

## Arguments
[@WorkerAgentId =] *WorkerAgentId*  
The worker agent ID of Scale Out Worker. The *WorkerAgentId* is **uniqueidentifier**.

[@PropertyName =] *PropertyName*  
The name of the property. The *PropertyName* is **nvarchar(256)**.

[@PropertyValue =] *PropertyValue*  
The value of the property. The *PropertyValue* is **nvarchar(max)**.

## Remarks
The valid property names are **DisplayName**, **Description**, **Tags**.

## Return Code Value  
 0 (success)  
  
## Result Sets  
 None  

## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role

## Errors and Warnings
  The following list describes some conditions that may raise an error or warning:  
  
-   The user does not have the appropriate permissions 

-   The worker agent ID is not valid.

-   The property name is not valid.

-   The property value is not valid.  
