---
title: "sp_help_peerconflictdetection (Transact-SQL)"
description: "sp_help_peerconflictdetection (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "sp_help_peerconflictdetection"
  - "sp_help_peerconflictdetection_TSQL"
helpviewer_keywords:
  - "sp_help_peerconflictdetection"
dev_langs:
  - "TSQL"
---
# sp_help_peerconflictdetection (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns information about the conflict detection settings for a publication that is involved in a peer-to-peer transactional replication topology.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_help_peerconflictdetection [ @publication = ] 'publication'  
    [ ,[ @timeout = ] timeout ]  
```  
  
## Arguments  
 [ @publication= ] '*publication*'  
 Is the name of the publication for which to return information. *publication* is **sysname**, with no default.  
  
 [ @timeout= ] *timeout*  
 Specifies the amount of time, in seconds, after which the procedure will time out while waiting for response from every node in the topology. If there is a read-only Subscriber in the topology, specifying a time-out value is not valid. Read-only Subscribers will never respond to a call from this procedure. *timeout* is **int**, with a default of 60.  
  
## Result Sets  
 sp_help_peerconflictdetection returns three result sets. These results are documented in the following topics:  
  
-   [MSpeer_conflictdetectionconfigrequest](../../relational-databases/system-tables/mspeer-conflictdetectionconfigrequest-transact-sql.md)  
  
-   [MSpeer_conflictdetectionconfigresponse](../../relational-databases/system-tables/mspeer-conflictdetectionconfigresponse-transact-sql.md)  
  
-   [Mspeer_originatorid_history](../../relational-databases/system-tables/mspeer-originatorid-history-transact-sql.md)  
  
## Return Code Values  
 **0** (success) or **1** (failure)  
  
## Remarks  
 sp_help_peerconflictdetection is used in peer-to-peer transactional replication.  
  
## Permissions  
 Requires membership in the sysadmin fixed server role or db_owner fixed database role.  
  
## See Also  
 [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md)   
 [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md)   
 [Replication Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
