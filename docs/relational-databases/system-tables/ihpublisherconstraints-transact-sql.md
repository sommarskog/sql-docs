---
title: "IHpublisherconstraints (Transact-SQL)"
description: IHpublisherconstraints (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "IHpublisherconstraints"
  - "IHpublisherconstraints_TSQL"
helpviewer_keywords:
  - "IHpublisherconstraints system table"
dev_langs:
  - "TSQL"
---
# IHpublisherconstraints (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **IHpublisherconstraints** system table contains one row for each constraint replicated from non-SQL Server Publishers using the current Distributor. This table is stored in the distribution database.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**publisherconstraint_id**|**int**|Identifies a published constraint.|  
|**table_id**|**int**|Identifies the table from [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) to which the constraint belongs.|  
|**publisher_id**|**smallint**|Identifies the non-SQL Server Publisher from which the column is being published.|  
|**Name**|**Sysname**|The name of the published constraint.|  
|**Type**|**nvarchar(255)**|A supported constraint type from the [IHconstrainttypes](../../relational-databases/system-tables/ihconstrainttypes-transact-sql.md) system table.|  
  
## See Also  
 [Heterogeneous Database Replication](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
