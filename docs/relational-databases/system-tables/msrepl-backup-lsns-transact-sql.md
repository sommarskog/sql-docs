---
title: "MSrepl_backup_lsns (Transact-SQL)"
description: MSrepl_backup_lsns (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "MSrepl_backup_lsns_TSQL"
  - "MSrepl_backup_lsns"
helpviewer_keywords:
  - "MSrepl_backup_Isns system table"
dev_langs:
  - "TSQL"
---
# MSrepl_backup_lsns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **MSrepl_backup_lsns** table contains transaction log sequence numbers (LSN) for supporting the 'sync with backup' option of the Distribution database. This table is stored in the distribution database.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**publisher_database_id**|**int**|The ID of the Publisher database.|  
|**valid_xact_id**|**varbinary(16)**|The ID of the transaction to be sent to the Publisher to mark the log truncation point. Used only if the Distribution database is in 'sync with backup' mode. Contains the ID of the latest replicated transaction in the Distribution database that has been backed up. It will be sent to the Publisher to mark the log truncation point by the Log Reader.|  
|**valid_xact_seqno**|**varbinary(16)**|The Sequence number of the transaction to be sent to the Publisher to mark the log truncation point. This is used only if the Distribution database is in 'sync with backup' mode. It is the log sequence number of the latest replication transaction in the Distribution database that has been backed up. It will be sent to the Publisher to mark the log truncation point by the Log Reader.|  
|**next_xact_id**|**varbinary(16)**|The temporary log sequence number used by backup operations.|  
|**nextx_xact_seqno**|**varbinary(16)**|The temporary log sequence number used by backup operations.|  
  
## See Also  
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
