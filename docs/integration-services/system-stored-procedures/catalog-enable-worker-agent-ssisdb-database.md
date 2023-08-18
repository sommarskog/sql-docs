---
title: "catalog.enable_worker_agent (SSISDB Database)"
description: "catalog.enable_worker_agent (SSISDB Database)"
author: chugugrace
ms.author: chugu
ms.date: "12/16/2016"
ms.service: sql
ms.subservice: integration-services
ms.topic: conceptual
---
# catalog.enable_worker_agent (SSISDB Database)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

Enable a Scale Out Worker for Scale Out Master working with this [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] catalog.

## Syntax

```sql
catalog.enable_worker_agent [ @WorkerAgentId = ] WorkerAgentId
```
## Arguments
[@WorkerAgentId =] *WorkerAgentId*
The worker agent ID of Scale Out Worker. The *WorkerAgentId* is **uniqueidentifier**.

## Example
This example enables the Scale Out Worker on MachineA.

```sql
SELECT WorkerAgentId, MachineName FROM [catalog].[worker_agents]
GO
-- Result: --
-- WorkerAgentId                           MachineName --
-- 6583054A-E915-4C2A-80E4-C765E79EF61D    MachineA    --

EXEC [catalog].[enable_worker_agent] '6583054A-E915-4C2A-80E4-C765E79EF61D'
GO 
```

## Return Code Value  
 0 (success)  
  
## Result Sets  
 None  

## Permissions  
 This stored procedure requires one of the following permissions:  
  
-   Membership to the **ssis_admin** database role  
  
-   Membership to the **sysadmin** server role 

## Errors and Warnings
If the worker agent ID is not valid, the stored procedure returns an error.
