---
title: "MSpeer_lsns (Transact-SQL)"
description: MSpeer_lsns (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "MSpeer_lsns"
  - "MSpeer_lsns_TSQL"
helpviewer_keywords:
  - "MSpeer_lsns system table"
dev_langs:
  - "TSQL"
---
# MSpeer_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **Mspeer_lsns** table is used to map each transaction to a subscription in a peer-to-peer replication topology. This table is stored in every publication database in a peer-to-peer replication topology and in the subscription database of all Subscribers to a peer-to-peer publication. For more information on this type of transactional replication topology, see [Peer-to-Peer Transactional Replication](../../relational-databases/replication/transactional/peer-to-peer-transactional-replication.md). This table is stored in the publication database.  
  
## Definition  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Identifies a peer-to-peer LSN.|  
|**last_updated**|**datetime**|The **datetime** at which the last row update was made.|  
|**originator**|**sysname**|The name of the Publisher that originated the transaction.|  
|**originator_db**|**sysname**|The name of the database in which the transaction originated.|  
|**originator_publication**|**sysname**|The name of the publication in which the transaction originated.|  
|**originator_publication_id**|**int**|The identifier for the publication in which the transaction originated.|  
|**originator_db_version**|**int**|Identifies the version number of the originating database.|  
|**originator_lsn**|**int**|Identifies the LSN in the originating publication.|  
|**originator_version**|**int**|Identifies the version number of the Publisher.|  
|**originator_id**|**smallint**|Identifies each node in the topology for the purposes of conflict detection. For more information, see [Conflict Detection in Peer-to-Peer Replication](../../relational-databases/replication/transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).|  
  
## See Also  
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
