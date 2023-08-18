---
title: "sys.dm_pdw_wait_stats (Transact-SQL)"
description: sys.dm_pdw_wait_stats (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest"
---
# sys.dm_pdw_wait_stats (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Holds information related to the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OS state related to instances running on the different nodes. For a list of waits types and their description, see [sys.dm_os_wait_stats](https://msdn.microsoft.com/library/ms179984\(v=sql.120\).aspx).

> [!NOTE]
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|**pdw_node_id**|**int**|ID of the node this entry refers to.||  
|**wait_name**|**nvarchar(255)**|Name of the wait type.||  
|**max_wait_time**|**bigint**|Maximum wait time of this wait type.||  
|**request_count**|**bigint**|Number of waits of this wait type outstanding.||  
|**signal_time**|**bigint**|Difference between the time that the waiting thread was signaled and when it started running.||  
|**completed_count**|**bigint**|Total number of waits of this type completed since the last server restart.||  
|**wait_time**|**bigint**|Total wait time for this wait type in millisecons. Inclusive of signal_time.||  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)   
 [sys.dm_pdw_waits &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-waits-transact-sql.md)  
  
  
