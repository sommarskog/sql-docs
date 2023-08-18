---
title: "sp_help_operator (Transact-SQL)"
description: "sp_help_operator (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "08/01/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_help_operator"
  - "sp_help_operator_TSQL"
helpviewer_keywords:
  - "sp_help_operator"
dev_langs:
  - "TSQL"
---
# sp_help_operator (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Reports information about the operators defined for the server.  
  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_help_operator  
     { [ @operator_name = ] 'operator_name'   
     | [ @operator_id = ] operator_id }  
```  
  
## Arguments  
`[ @operator_name = ] 'operator_name'`
 The operator name. *operator_name* is **sysname**. If *operator_name* is not specified, information about all operators is returned.  
  
`[ @operator_id = ] operator_id`
 The identification number of the operator for which information is requested. *operator_id*is **int**, with a default of NULL.  
  
> [!NOTE]  
>  Either *operator_id* or *operator_name* must be specified, but both cannot be specified.  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Operator identification number.|  
|**name**|**sysname**|Operator Name.|  
|**enabled**|**tinyint**|Operator is available to receive any notifications:<br /><br /> **1** = Yes<br /><br /> **0** = No|  
|**email_address**|**nvarchar(100)**|Operator e-mail address.|  
|**last_email_date**|**int**|Date the operator was last notified by e-mail.|  
|**last_email_time**|**int**|Time the operator was last notified by e-mail.|  
|**pager_address**|**nvarchar(100)**|Operator pager address.|  
|**last_pager_date**|**int**|Date the operator was last notified by pager.|  
|**last_pager_time**|**int**|Time the operator was last notified by pager.|  
|**weekday_pager_start_time**|**int**|The start of the time period during which the operator is available to receive pager notifications on a weekday.|  
|**weekday_pager_end_time**|**int**|The end of the time period during which the operator is available to receive pager notifications on a weekday.|  
|**saturday_pager_start_time**|**int**|The start of the time period during which the operator is available to receive pager notifications on Saturdays.|  
|**saturday_pager_end_time**|**int**|The end of the time period during which the operator is available to receive pager notifications on Saturdays.|  
|**sunday_pager_start_time**|**int**|The start of the time period during which the operator is available to receive pager notifications on Sundays.|  
|**sunday_pager_end_time**|**int**|The end of the time period during which the operator is available to receive pager notifications on Sundays.|  
|**pager_days**|**tinyint**|A bitmask (**1** = Sunday, **64** = Saturday) of days-of-the week indicating when the operator is available to receive pager notifications.|  
|**netsend_address**|**nvarchar(100)**|Operator address for network pop-up notifications.|  
|**last_netsend_date**|**int**|Date the operator was last notified by network pop-up.|  
|**last_netsend_time**|**int**|Time the operator was last notified by network pop-up.|  
|**category_name**|**sysname**|Name of the operator category to which this operator belongs.|  
  
## Remarks  
 **sp_help_operator** must be run from the **msdb** database.  
  
## Permissions  
 By default, members of the **sysadmin** fixed server role can execute this stored procedure. Other users must be granted one of the following [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent fixed database roles in the **msdb** database:  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
 For details about the permissions of these roles, see [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## Examples  
 The following example reports information about operator `François Ajenstat`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_help_operator  
    @operator_name = N'François Ajenstat' ;  
GO  
```  
  
## See also  
 [sp_add_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-operator-transact-sql.md)   
 [sp_delete_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-operator-transact-sql.md)   
 [sp_update_operator &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-update-operator-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
