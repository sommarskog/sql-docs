---
title: "sp_delete_maintenance_plan_job (Transact-SQL)"
description: "sp_delete_maintenance_plan_job (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_delete_maintenance_plan_job"
  - "sp_delete_maintenance_plan_job_TSQL"
helpviewer_keywords:
  - "sp_delete_maintenance_plan_job"
dev_langs:
  - "TSQL"
---
# sp_delete_maintenance_plan_job (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Disassociates the specified maintenance plan from the specified job.  
  
> [!NOTE]  
>  This stored procedure is used with database maintenance plans. This feature has been replaced with maintenance plans which do not use this stored procedure. Use this procedure to maintain database maintenance plans on installations that were upgraded from a previous version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_delete_maintenance_plan_job [ @plan_id = ] 'plan_id' ,   
   [ @job_id = ] 'job_id'   
```  
  
## Arguments  
`[ @plan_id = ] 'plan\_id'`
 Specifies the ID of the maintenance plan. *plan_id* is **uniqueidentifier**, and must be a valid ID.  
  
`[ @job_id = ] 'job\_id'`
 Specifies the ID of the job with which the maintenance plan is associated. *job_id* is **uniqueidentifier**, and must be a valid ID.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Remarks  
 **sp_delete_maintenance_plan_job** must be run from the **msdb** database.  
  
 When all jobs have been removed from the maintenance plan, we recommend that users execute **sp_delete_maintenance_plan_db** to remove the remaining databases from the plan.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_delete_maintenance_plan_job**.  
  
## Examples  
 This example deletes the job "B8FCECB1-E22C-11D2-AA64-00C04F688EAE" from the maintenance plan.  
  
```  
EXECUTE   sp_delete_maintenance_plan_job N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC', N'B8FCECB1-E22C-11D2-AA64-00C04F688EAE';  
```  
  
## See Also  
 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Database Maintenance Plan Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
