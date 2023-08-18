---
title: "sys.dm_pdw_os_event_logs (Transact-SQL)"
description: sys.dm_pdw_os_event_logs (Transact-SQL)
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
# sys.dm_pdw_os_event_logs (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Holds information regarding the different Windows Event logs on the different nodes.  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|Appliance node this log is from.<br /><br /> pdw_node_id and log_name form the key for this view.||  
|log_name|**nvarchar(255)**|Windows event log name.<br /><br /> pdw_node_id and log_name form the key for this view.||  
|log_source|**nvarchar(255)**|Windows event log source name.||  
|event_id|**int**|ID of the event. Not unique.||  
|event_type|**nvarchar(255)**|Type of the event, identifying severity.|'Information', 'Warning', 'Error'|  
|event_message|**nvarchar(4000)**|Details of the event.||  
|generate_time|**datetime**|Time the event was created.||  
|write_time|**datetime**|Time the event was actually written to the log.||  
  
 For information about the maximum rows retained by this view, see the Metadata section in the [Capacity limits](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) topic. 
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
