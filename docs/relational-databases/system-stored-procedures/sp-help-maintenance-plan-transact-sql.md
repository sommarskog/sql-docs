---
title: "sp_help_maintenance_plan (Transact-SQL)"
description: "sp_help_maintenance_plan (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "08/09/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_help_maintenance_plan_TSQL"
  - "sp_help_maintenance_plan"
helpviewer_keywords:
  - "sp_help_maintenance_plan"
dev_langs:
  - "TSQL"
---
# sp_help_maintenance_plan (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns information about the specified maintenance plan. If a plan is not specified, this stored procedure returns information about all maintenance plans.  
  
> [!NOTE]  
> This stored procedure is used with database maintenance plans. This feature has been replaced with maintenance plans which do not use this stored procedure. Use this procedure to maintain database maintenance plans on installations that were upgraded from a previous version of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_help_maintenance_plan [ [ @plan_id = ] 'plan_id' ]  
```  
  
## Arguments  
`[ @plan_id = ] 'plan\_id'`
 Specifies the plan ID of the maintenance plan. *plan_id* is **UNIQUEIDENTIFIER**. The default is NULL.  
  
## Return Code Values  
 None  
  
## Result Sets  
 If *plan_id* is specified, **sp_help_maintenance_plan** will return three tables: Plan, Database, and Job.  
  
### Plan Table  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**plan_id**|**uniqueidentifier**|Maintenance plan ID.|  
|**plan_name**|**sysname**|Maintenance plan name.|  
|**date_created**|**datetime**|Date the maintenance plan was created.|  
|**owner**|**sysname**|Owner of the maintenance plan.|  
|**max_history_rows**|**int**|Maximum number of rows allocated for recording the history of the maintenance plan in the system table.|  
|**remote_history_server**|**int**|The name of the remote server to which the history report could be written.|  
|**max_remote_history_rows**|**int**|Maximum number of rows allocated in the system table on a remote server to which the history report could be written.|  
|**user_defined_1**|**int**|Default is NULL.|  
|**user_defined_2**|**nvarchar(100)**|Default is NULL.|  
|**user_defined_3**|**datetime**|Default is NULL.|  
|**user_defined_4**|**uniqueidentifier**|Default is NULL.|  
  
### Database Table  
  
|Column name|Description|  
|-----------------|-----------------|  
|**database_name**|Name of all databases associated with the maintenance plan. *database_name* is **sysname**.|  
  
### Job Table  
  
|Column name|Description|  
|-----------------|-----------------|  
|**job_id**|ID of all jobs associated with the maintenance plan. *job_id* is **uniqueidentifier**.|  
  
## Remarks  
 **sp_help_maintenance_plan** is in the **msdb** database.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_help_maintenance_plan**.  
  
## Examples  
 This example descriptive information about the maintenance plan FAD6F2AB-3571-11D3-9D4A-00C04FB925FC.  
  
```  
EXECUTE   sp_help_maintenance_plan   
   N'FAD6F2AB-3571-11D3-9D4A-00C04FB925FC';  
```  
  
## See Also  
 [Maintenance Plans](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Database Maintenance Plan Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-maintenance-plan-stored-procedures-transact-sql.md)  
  
  
