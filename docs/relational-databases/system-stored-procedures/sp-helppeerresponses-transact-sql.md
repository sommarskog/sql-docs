---
title: "sp_helppeerresponses (Transact-SQL)"
description: "sp_helppeerresponses (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_helppeerresponses_TSQL"
  - "sp_helppeerresponses"
helpviewer_keywords:
  - "sp_helppeerresponses"
dev_langs:
  - "TSQL"
---
# sp_helppeerresponses (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns all responses to a specific status request received from a participant in a peer-to-peer replication topology, where the request was initiated by executing [sp_helppeerrequests](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) at any published database in the topology. This stored procedure is executed on the publication database at a Publisher participating in a peer-to-peer replication topology. For more information, see [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_helppeerresponses [ @request_id = ] request_id  
```  
  
## Arguments  
`[ @request_id = ] request_id`
 Is the ID of a specific status request. *request_id* is **int**, with no default.  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**request_id**|**int**|ID of the status request.|  
|**peer**|**sysname**|The name of the peer that generated the response.|  
|**peer_db**|**sysname**|The database name at the peer that generated the response.|  
|**received_date**|**datetime**|Date and time that the requestor received the response from the peer that sent it.|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_helppeerresponses** is used in peer-to-peer transactional replication.  
  
 **sp_helppeerresponses** procedure is used when restoring a database published in a peer-to-peer topology.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or the **db_owner** fixed database role can execute **sp_helppeerresponses**.  
  
## See Also  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerrequests &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerrequests-transact-sql.md)  
  
  
