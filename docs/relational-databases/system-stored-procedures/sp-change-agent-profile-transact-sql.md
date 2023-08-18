---
title: "sp_change_agent_profile (Transact-SQL)"
description: "sp_change_agent_profile (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_change_agent_profile"
  - "sp_change_agent_profile_TSQL"
helpviewer_keywords:
  - "sp_change_agent_profile"
dev_langs:
  - "TSQL"
---
# sp_change_agent_profile (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Changes a parameter of a replication agent profile stored in the [MSagent_profiles &#40;Transact-SQL&#41;](../../relational-databases/system-tables/msagent-profiles-transact-sql.md) table. This stored procedure is executed at the Distributor on any database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_change_agent_profile [ @profile_id = ] profile_id   
        , [ @property = ] 'property'   
        , [ @value = ] 'value'   
```  
  
## Arguments  
`[ @profile_id = ] profile_id`
 Is the ID of the profile. *profile_id* is **int**, with no default.  
  
`[ @property = ] 'property'`
 Is the name of the property. *property* is **sysname**, with no default.  
  
`[ @value = ] 'value'`
 Is the new value of the property. *value* is **nvarchar(3000)**, with no default.  
  
 This table describes the profile properties that can be changed.  
  
|Property|Description|  
|--------------|-----------------|  
|**description**|Description for the profile.|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_change_agent_profile** is used in all types of replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_change_agent_profile**.  
  
## See Also  
 [sp_add_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-agent-profile-transact-sql.md)   
 [sp_drop_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-drop-agent-profile-transact-sql.md)   
 [sp_help_agent_profile &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-agent-profile-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
