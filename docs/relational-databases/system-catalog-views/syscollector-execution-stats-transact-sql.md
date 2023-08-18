---
title: "syscollector_execution_stats (Transact-SQL)"
description: syscollector_execution_stats (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/10/2016"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "syscollector_execution_stats"
  - "syscollector_execution_stats_TSQL"
helpviewer_keywords:
  - "syscollector_execution_stats view"
  - "data collector view"
dev_langs:
  - "TSQL"
---
# syscollector_execution_stats (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Provides information about task execution for a collection set or package.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|Identifies each collection set execution. Used to join this view with other detailed logs. Is not nullable.|  
|**task_name**|**nvarchar(128)**|The name of the collection set or package task that this information is for. Is not nullable.|  
|**execution_row_count_in**|**int**|Number of rows processed at the beginning of data flow. Is nullable.|  
|**execution_row_count_out**|**int**|Number of rows processed at the end of data flow. Is nullable.|  
|**execution_row_count_errors**|**int**|Number of rows that failed during the data flow. Is nullable.|  
|**execution_time_ms**|**int**|The time, in milliseconds, required for the task to complete. Is nullable.|  
|**log_time**|**datetime**|The time that this information was logged. Is not nullable.|  
  
## Permissions  
 Requires SELECT permission for **dc_operator**.  
  
## See Also  
 [Data Collector Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Data Collector Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [Data Collection](../../relational-databases/data-collection/data-collection.md)  
  
  
