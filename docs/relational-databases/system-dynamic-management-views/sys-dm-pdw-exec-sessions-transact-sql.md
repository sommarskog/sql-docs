---
title: "sys.dm_pdw_exec_sessions (Transact-SQL)"
description: sys.dm_pdw_exec_sessions (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/22/2019"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest"
---
# sys.dm_pdw_exec_sessions (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Holds information about all sessions currently or recently open on the appliance. It lists one row per session. 

> [!NOTE]
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)] For serverless SQL pool use [sys.dm_exec_sessions (Transact-SQL)](sys-dm-exec-sessions-transact-sql.md).
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|session_id|**nvarchar(32)**| The ID of of the current query or the last query run (if the session is TERMINATED and the query was executing at time of termination). Key for this view.|Unique across all sessions in the system.|  
|status|**nvarchar(10)**|For current sessions, identifies whether the session is currently active or idle. For past sessions, the session status may show closed or killed (if the session was forcibly closed).|'ACTIVE', 'CLOSED', 'IDLE', 'TERMINATED'|  
|request_id|**nvarchar(32)**|The ID of the current query or last query run.|Unique across all requests in the system. Null if none has been run.|  
|security_id|**varbinary(85)**|Security ID of the principal running the session.||  
|login_name|**nvarchar(128)**|The login name of the principal running the session.|Any string conforming to the user naming conventions.|  
|login_time|**datetime**|Date and time at which the user logged in and this session was created.|Valid **datetime** before current time.|  
|query_count|**int**|Captures the number of queries/requeststhis session has run since creation.|Greater than or equal to 0.|  
|is_transactional|**bit**|Captures whether a session is currently within a transaction or not.|0 for auto-commit, 1 for transactional.|  
|client_id|**nvarchar(255)**|Captures client information for the session. IPv6 address indicates private endpoint is used.|Any valid string.|  
|app_name|**nvarchar(255)**|Captures application name information optionally set as part of the connection process.|Any valid string.|  
|sql_spid|**int**|The IDs column contains closed SPIDs.||  
  
 For information about the maximum rows retained by this view, see the Metadata section in the [Capacity limits](/azure/sql-data-warehouse/sql-data-warehouse-service-capacity-limits#metadata) topic.  
  
## Permissions  
 Requires the `VIEW SERVER STATE` permission.  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
