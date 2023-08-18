---
title: "logmarkhistory (Transact-SQL)"
description: logmarkhistory (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "logmarkhistory"
  - "logmarkhistory_TSQL"
helpviewer_keywords:
  - "logmarkhistory system table"
dev_langs:
  - "TSQL"
---
# logmarkhistory (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Contains one row for each marked transaction that has been committed. This table is stored in the **msdb** database.  
  

|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Local database where marked transaction occurred.|  
|**mark_name**|**nvarchar(128)**|User-provided name for marked transaction.|  
|**description**|**nvarchar(255)**|User-provided description of the marked transaction. Can be NULL.|  
|**user_name**|**nvarchar(128)**|Database user name that performed marked transaction. Can be NULL.|  
|**lsn**|**numeric(25,0)**|Log sequence number of transaction record where mark occurred.|  
|**mark_time**|**datetime**|Commit time of marked transaction (local time).|  
  
## See Also  
 [Restore a Database to a Marked Transaction &#40;SQL Server Management Studio&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-marked-transaction-sql-server-management-studio.md)   
 [Use Marked Transactions to Recover Related Databases Consistently &#40;Full Recovery Model&#41;](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)   
 [System Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)  
  
  
