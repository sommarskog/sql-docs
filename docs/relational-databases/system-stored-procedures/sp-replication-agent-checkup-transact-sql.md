---
title: "sp_replication_agent_checkup (Transact-SQL)"
description: "sp_replication_agent_checkup (Transact-SQL)"
author: MashaMSFT
ms.author: mathoma
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_replication_agent_checkup_TSQL"
  - "sp_replication_agent_checkup"
helpviewer_keywords:
  - "sp_replication_agent_checkup"
dev_langs:
  - "TSQL"
---
# sp_replication_agent_checkup (Transact-SQL)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

  Checks each distribution database for replication agents that are running but have not logged history within the specified heartbeat interval. This stored procedure is executed at the Distributor on any database.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_replication_agent_checkup [ [ @heartbeat_interval = ] heartbeat_interval ]  
```  
  
## Arguments  
`[ @heartbeat_interval = ] 'heartbeat_interval'`
 Is the maximum number of minutes that an agent can go without logging a progress message. *heartbeat_interval* is **int**, with a default of 10 minutes.  
  
## Return Code Values  
 **sp_replication_agent_checkup** raises error 14151 for each agent it detects as suspect. It also logs a failure history message about the agents.  
  
## Remarks  
 **sp_replication_agent_checkup** is used in snapshot replication, transactional replication, and merge replication.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role can execute **sp_replication_agent_checkup**.  
  
## See Also  
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
