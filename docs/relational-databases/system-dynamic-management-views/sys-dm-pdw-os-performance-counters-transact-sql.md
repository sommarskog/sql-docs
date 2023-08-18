---
title: "sys.dm_pdw_os_performance_counters (Transact-SQL)"
description: sys.dm_pdw_os_performance_counters (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/07/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016"
---
# sys.dm_pdw_os_performance_counters (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Contains information about Windows performance counters for the nodes in [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|The ID of the node that contains the counter.<br /><br /> pdw_node_id and counter_name form the key for this view.|See node_id in [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|counter_name|**nvarchar(255)**|Name of Windows performance counter.||  
|counter_category|**nvarchar(255)**|Name of Windows performance counter category.||  
|instance_name|**nvarchar(255)**|Name of the specific instance of the counter.||  
|counter_value|**Decimal(38,10)**|Current value of the counter.||  
|last_update_time|**Datetime2(3)**|Timestamp of last time the value was updated.||  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
