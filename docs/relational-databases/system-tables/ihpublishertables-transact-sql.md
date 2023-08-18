---
title: "IHpublishertables (Transact-SQL)"
description: IHpublishertables (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "IHpublishertables"
  - "IHpublishertables_TSQL"
helpviewer_keywords:
  - "IHpublishertables system table"
dev_langs:
  - "TSQL"
---
# IHpublishertables (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **IHpublishertables** system table represents metadata stored at the publisher. This table contains one row for each source table published from a non-SQL Server Publisher using the current Distributor. This table is stored in the distribution database.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|Identifies a published table.|  
|**publisher_id**|**smallint**|Identifies the non-SQL Server Publisher from which the table is being published.|  
|**name**|**sysname**|The name of the published table.|  
|**owner**|**sysname**|The table owner.|  
  
## See Also  
 [Heterogeneous Database Replication](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
