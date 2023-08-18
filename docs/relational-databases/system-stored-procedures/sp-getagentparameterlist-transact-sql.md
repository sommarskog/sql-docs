---
title: "sp_getagentparameterlist (Transact-SQL)"
description: "sp_getagentparameterlist (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_getagentparameterlist"
  - "sp_getagentparameterlist_TSQL"
helpviewer_keywords:
  - "sp_getagentparameterlist"
dev_langs:
  - "TSQL"
---
# sp_getagentparameterlist (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns a list of all replication agent parameters that can be set in an agent profile for the specified agent type. This stored procedure is executed at the Distributor where the agent is running, on any database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_getagentparameterlist [ @agent_type = ] 'agent_type'  
```  
  
## Arguments  
`[ @agent_type = ] 'agent_type'`
 Is the replication agent for which the parameter is being added. *agent_type* is **int**, and can be one of these values:  
  
|Value|Agent|  
|-----------|-----------|  
|**1**|Snapshot|  
|**2**|Log Reader|  
|**3**|Distribution|  
|**4**|Merge|  
|**9**|Queue Reader|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_getagentparameter**.  
  
## See Also  
 [sp_add_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-parameter-transact-sql.md)   
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-parameter-transact-sql.md)   
 [sp_help_agent_parameter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-parameter-transact-sql.md)   
 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
