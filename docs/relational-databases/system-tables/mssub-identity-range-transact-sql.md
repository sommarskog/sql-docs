---
title: "MSsub_identity_range (Transact-SQL)"
description: MSsub_identity_range (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "MSsub_identity_range_TSQL"
  - "MSsub_identity_range"
helpviewer_keywords:
  - "MSsub_identity_range system table"
dev_langs:
  - "TSQL"
---
# MSsub_identity_range (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **MSsub_identity_range** table provides identity range management support for subscriptions. This table is stored in the subscription databases.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**objid**|**int**|The ID of the table that has the identity column being managed by replication.|  
|**range**|**bigint**|Controls the range size of the consecutive identity values that would be assigned at the Subscriber in an adjustment.|  
|**last_seed**|**bigint**|The lower bound of the current range.|  
|**threshold**|**int**|The percentage value that controls when the Distribution Agent assigns a new identity range. When the percentage of values specified in *threshold* is used, the Distribution Agent creates a new identity range.|  
  
## See Also  
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
