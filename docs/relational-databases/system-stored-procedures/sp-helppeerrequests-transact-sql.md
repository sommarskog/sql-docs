---
title: "sp_helppeerrequests (Transact-SQL)"
description: "sp_helppeerrequests (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_helppeerrequests_TSQL"
  - "sp_helppeerrequests"
helpviewer_keywords:
  - "sp_helppeerrequests"
dev_langs:
  - "TSQL"
---
# sp_helppeerrequests (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns information on all status requests received by participants in a peer-to-peer replication topology, where these requests were initiated by executing [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md) at any published database in the topology. This stored procedure is executed on the publication database at a Publisher participating in a peer-to-peer replication topology. For more information, see [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md).  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_helppeerrequests [ @publication = ] 'publication'  
    [ , [ @description = ] 'description'  
```  
  
## Arguments  
`[ @publication = ] 'publication'`
 Is the name of the publication in a peer-to-peer topology for which status requests were sent. *publication* is **sysname**, with no default.  
  
`[ @description = ] 'description'`
 Value that can be used to identify individual status requests, which enables you to filter returned responses based on user defined information supplied when calling [sp_requestpeerresponse &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-requestpeerresponse-transact-sql.md). *description* is **nvarchar(4000)**, with a default of **%**. By default, all status requests for the publication are returned. This parameter is used to return only status requests with a description matching the value supplied in *description*, where character strings are matched using a [LIKE &#40;Transact-SQL&#41;](../../t-sql/language-elements/like-transact-sql.md) clause.  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifies a request.|  
|**publication**|**sysname**|Name of the publication for which the status request was sent.|  
|**sent_date**|**datetime**|Date and time that the status request was sent.|  
|**description**|**nvarchar(4000)**|User defined information that can be used to identify individual status requests.|  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 **sp_helppeerrequests** is used in peer-to-peer transactional replication.  
  
 **sp_helppeerrequests** is used when restoring a database published in a peer-to-peer topology.  
  
## Permissions  
 Only members of the **sysadmin** fixed server role or the **db_owner** fixed database role can execute **sp_helppeerrequests**.  
  
## See Also  
 [sp_deletepeerrequesthistory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-deletepeerrequesthistory-transact-sql.md)   
 [sp_helppeerresponses &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helppeerresponses-transact-sql.md)  
  
  
