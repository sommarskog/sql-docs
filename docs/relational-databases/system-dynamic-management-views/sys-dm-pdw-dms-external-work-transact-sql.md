---
title: "sys.dm_pdw_dms_external_work (Transact-SQL)"
description: sys.dm_pdw_dms_external_work (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest"
---
# sys.dm_pdw_dms_external_work (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] system view that holds information about all Data Movement Service (DMS) steps for external operations.

> [!NOTE]
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|request_id|**nvarchar(32)**|Query that is using this DMS worker.<br /><br /> request_id, step_index, and dms_step_index form the key for this view.|Same as request_id in [sys.dm_pdw_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md).|  
|step_index|**int**|Query step that is invoking this DMS worker.<br /><br /> request_id, step_index, and dms_step_index form the key for this view.|Same as step_index in [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|dms_step_index|**int**|Current step in the DMS plan.<br /><br /> request_id, step_index, and dms_step_index form the key for this view.|Same as dms___step_index in [sys.dm_pdw_dms_workers &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-dms-workers-transact-sql.md).|  
|pdw_node_id|**int**|Node that is running the DMS worker.|Same as node_id in [sys.dm_pdw_nodes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md).|  
|type|**nvarchar(60)**|Type of external operation this node is running.<br /><br /> FILE SPLIT is an operation on an external Hadoop file that has been split into multiple smaller falls.|'FILE SPLIT'|  
|work_id|**int**|The file split ID.|Greater than or equal to 0.<br /><br /> Unique per Compute node.|  
|input_name|**nvarchar(60)**|String name for the input being read.|For a Hadoop file, this is the Hadoop file name.|  
|read_location|**bigint**|Offset of read location.||  
|bytes_processed|**bigint**|Number of bytes processed by this worker.|Greater than or equal to 0.|  
|length|**bigint**|Number of bytes in the file split.<br /><br /> For Hadoop, this is the size of the HDFS block.|User-defined. The default is 64 MB.|  
|status|**nvarchar(32)**|State of the worker.|Pending, Processing, Done, Failed, Aborted|  
|start_time|**datetime**|Time at which execution of this worker started.|Greater than or equal to start time of the query step this worker belongs to. See [sys.dm_pdw_request_steps &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md).|  
|end_time|**datetime**|Time at which execution ended, failed, or was canceled.|NULL for ongoing or queued workers. Otherwise, greater than start_time.|  
|total_elapsed_time|**int**|Total time spent in execution, in milliseconds.|Greater than or equal to 0.<br /><br /> If total_elapsed_time exceeds the maximum value for an integer, total_elapsed_time will continue to be the maximum value. This condition will generate the warning "The maximum value has been exceeded."<br /><br /> The maximum value in milliseconds is equivalent to 24.8 days.|  
  
 For information about the maximum rows retained by this view, see the Metadata section in the [Capacity limits](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) topic.
  
## See Also  
 [System Views &#40;Transact-SQL&#41;](../../t-sql/language-reference.md)  
  
