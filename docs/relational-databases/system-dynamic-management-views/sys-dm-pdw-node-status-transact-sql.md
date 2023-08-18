---
title: "sys.dm_pdw_node_status (Transact-SQL)"
description: sys.dm_pdw_node_status (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/07/2017"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016"
---
# sys.dm_pdw_node_status (Transact-SQL)

[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Holds additional information (over [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) about the performance and status of all appliance nodes. It lists one row per node in the appliance.  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Unique numeric id associated with the node.<br /><br /> Key for this view.|Unique across the appliance, regardless of type.|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|Total allocated memory on this node.||  
|available_memory|**bigint**|Total available memory on this node.||  
|process_cpu_usage|**bigint**|Total process CPU usage, in ticks.||  
|total_cpu_usage|**bigint**|Total CPU usage, in ticks.||  
|thread_count|**bigint**|Total number of threads in use on this node.||  
|handle_count|**bigint**|Total number of handles in use on this node.||  
|total_elapsed_time|**bigint**|Total time elapsed since system start or restart.|Total time elapsed since system start or restart. If total_elapsed_time exceeds the maximum value for an integer (24.8 days in milliseconds), it will cause materialization failure due to overflow.<br /><br /> The maximum value in milliseconds is equivalent to 24.8 days.|  
|is_available|**bit**|Flag indicating whether this node is available.||  
|sent_time|**datetime**|Last time a network package was sent by this node.||  
|received_time|**datetime**|Last time a network package was received by this node.||  
|error_id|**nvarchar(36)**|Unique identifier of the last error that occurred on this node.||  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
