---
title: "MSmerge_errorlineage (Transact-SQL)"
description: MSmerge_errorlineage (Transact-SQL)
author: VanMSFT
ms.author: vanto
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: replication
ms.topic: "reference"
f1_keywords:
  - "MSmerge_errorlineage_TSQL"
  - "MSmerge_errorlineage"
helpviewer_keywords:
  - "MSmerge_errorlineage system table"
dev_langs:
  - "TSQL"
---
# MSmerge_errorlineage (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  The **MSmerge_errorlineage** table contains rows that have been deleted at the Subscriber, but whose delete is not propagated to the Publisher. This table is stored in the publication and subscription databases.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**tablenick**|**int**|The integer value assigned to the table that is published for merge replication. Corresponds to the nickname field in the **sysmergearticles** table.|  
|**rowguid**|**uniqueidentifier**|The row identifier.|  
|**lineage**|**varbinary(501)**|Stores a history list of which Subscribers and Publishers have made updates to a row. It is used to detect and resolve conflict situations.|  
  
## See Also  
 [Replication Tables &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Replication Views &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
