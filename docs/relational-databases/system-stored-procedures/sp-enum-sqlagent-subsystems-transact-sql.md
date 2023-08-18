---
title: "sp_enum_sqlagent_subsystems (Transact-SQL)"
description: "sp_enum_sqlagent_subsystems (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_enum_sqlagent_subsystems"
  - "sp_enum_sqlagent_subsystems_TSQL"
helpviewer_keywords:
  - "sp_enum_sqlagent_subsystems"
dev_langs:
  - "TSQL"
---
# sp_enum_sqlagent_subsystems (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Lists the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent subsystems.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_enum_sqlagent_subsystems  
```  
  
## Arguments  
 None  
  
## Return Code Values  
 **0** (success) or **1** (Failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**subsystem**|**nvarchar(40)**|Name of the subsystem.|  
|**description**|**nvarchar(512)**|Description of the subsystem.|  
|**subsystem_dll**|**nvarchar(510)**|DLL module that contains the subsystem.|  
|**agent_exe**|**nvarchar(510)**|Executable module that is used by the subsystem.|  
|**start_entry_point**|**nvarchar(30)**|Procedure that SQL Server Agent calls during job step execution.|  
|**event_entry_point**|**nvarchar(30)**|Procedure that SQL Server Agent calls during job step execution.|  
|**stop_entry_point**|**nvarchar(30)**|Procedure that SQL Server Agent calls during job step execution.|  
|**max_worker_threads**|**int**|Maximum number of threads [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent will start for this subsystem.|  
|**subsystem_id**|**int**|Identifier for the subsystem.|  
  
## Remarks  
 This procedure lists the subsystems available in the instance.  
  
## Permissions  
 By default, members of the **sysadmin** fixed server role can execute this stored procedure. Other users must be granted the **SQLAgentOperatorRole** fixed database role in the **msdb** database.  
  
 For details about **SQLAgentOperatorRole**, see [SQL Server Agent Fixed Database Roles](../../ssms/agent/sql-server-agent-fixed-database-roles.md).  
  
## See Also  
 [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_jobstep &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-jobstep-transact-sql.md)  
  
  
