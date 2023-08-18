---
title: "MSdynamicsnapshotviews (Transact-SQL)"
description: MSdynamicsnapshotviews (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/04/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "MSdynamicsnapshotviews_TSQL"
  - "MSdynamicsnapshotviews"
helpviewer_keywords:
  - "MSdynamicsnapshotviews system table"
dev_langs:
  - "TSQL"
---
# MSdynamicsnapshotviews (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **MSdynamicsnapshotviews** table tracks all the temporary filtered data snapshot views created by the snapshot agent, and is used by the system for cleaning up views in the case of an abnormal shutdown of SQL Server Agent or the Snapshot Agent. This table is stored in the publication and subscription databases.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**dynamic_snapshot_view_name**|**sysname**|The name of the temporary filtered data snapshot view.|  
  
## See Also  
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)  
  
  
