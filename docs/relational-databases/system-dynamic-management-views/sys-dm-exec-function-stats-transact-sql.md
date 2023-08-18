---
title: "sys.dm_exec_function_stats (Transact-SQL)"
description: sys.dm_exec_function_stats (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/19/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: conceptual
f1_keywords:
  - "sys.dm_exec_function_stats"
  - "sys.dm_exec_function_stats_tsql"
  - "dm_exec_function_stats"
  - "dm_exec_function_stats_tsql"
helpviewer_keywords:
  - "sys.dm_exec_function_stats dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_exec_function_stats (Transact-SQL)
[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Returns aggregate performance statistics for cached functions. The view returns one row for each cached function plan, and the lifetime of the row is as long as the function remains cached. When a  function is removed from the cache, the corresponding row is eliminated from this view. At that time, a Performance Statistics SQL trace event is raised similar to **sys.dm_exec_query_stats**. Returns information about scalar functions, including in-memory functions and CLR scalar functions. Does not return information about table valued functions, and about scalar functions that are inlined with [Scalar UDF Inlining](../../relational-databases/user-defined-functions/scalar-udf-inlining.md).
  
 In [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], dynamic management views cannot expose information that would impact database containment or expose information about other databases the user has access to. To avoid exposing this information, every row that contains data that doesn't belong to the connected tenant is filtered out.  
  
> [!NOTE]
> The results of **sys.dm_exec_function_stats**  may vary with each execution as the data only reflects finished queries, and not ones still in-flight. 

  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Database ID in which the function resides. <br /><br />In [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], the values are unique within a single database or an elastic pool, but not within a logical server.|  
|**object_id**|**int**|Object identification number of the function.|  
|**type**|**char(2)**|Type of the object:   FN = Scalar valued functions|  
|**type_desc**|**nvarchar(60)**|Description of the object type: SQL_SCALAR_FUNCTION|  
|**sql_handle**|**varbinary(64)**|This can be used to correlate with queries in **sys.dm_exec_query_stats** that were executed from within this function.|  
|**plan_handle**|**varbinary(64)**|Identifier for the in-memory plan. This identifier is transient and remains constant only while the plan remains in the cache. This value may be used with the **sys.dm_exec_cached_plans** dynamic management view.<br /><br /> Will always be 0x000 when a natively compiled function queries a memory-optimized table.|  
|**cached_time**|**datetime**|Time at which the function was added to the cache.|  
|**last_execution_time**|**datetime**|Last time at which the function was executed.|  
|**execution_count**|**bigint**|Number of times that the function has been executed since it was last compiled.|  
|**total_worker_time**|**bigint**|Total amount of CPU time, in microseconds, that was consumed by executions of this function since it was compiled.<br /><br /> For natively compiled functions, **total_worker_time** may not be accurate if many executions take less than 1 millisecond.|  
|**last_worker_time**|**bigint**|CPU time, in microseconds, that was consumed the last time the function was executed. <sup>1</sup>|  
|**min_worker_time**|**bigint**|Minimum CPU time, in microseconds, that this function has ever consumed during a single execution. <sup>1</sup>|  
|**max_worker_time**|**bigint**|Maximum CPU time, in microseconds, that this function has ever consumed during a single execution. <sup>1</sup>|  
|**total_physical_reads**|**bigint**|Total number of physical reads performed by executions of this function since it was compiled.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**last_physical_reads**|**bigint**|Number of physical reads performed the last time the function was executed.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**min_physical_reads**|**bigint**|Minimum number of physical reads that this function has ever performed during a single execution.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**max_physical_reads**|**bigint**|Maximum number of physical reads that this function has ever performed during a single execution.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**total_logical_writes**|**bigint**|Total number of logical writes performed by executions of this function since it was compiled.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**last_logical_writes**|**bigint**|Number of the number of buffer pool pages dirtied the last time the plan was executed. If a page is already dirty (modified) no writes are counted.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**min_logical_writes**|**bigint**|Minimum number of logical writes that this function has ever performed during a single execution.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**max_logical_writes**|**bigint**|Maximum number of logical writes that this function has ever performed during a single execution.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**total_logical_reads**|**bigint**|Total number of logical reads performed by executions of this function since it was compiled.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**last_logical_reads**|**bigint**|Number of logical reads performed the last time the function was executed.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**min_logical_reads**|**bigint**|Minimum number of logical reads that this function has ever performed during a single execution.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**max_logical_reads**|**bigint**|Maximum number of logical reads that this function has ever performed during a single execution.<br /><br /> Will always be 0 querying a memory-optimized table.|  
|**total_elapsed_time**|**bigint**|Total elapsed time, in microseconds, for completed executions of this function.|  
|**last_elapsed_time**|**bigint**|Elapsed time, in microseconds, for the most recently completed execution of this function.|  
|**min_elapsed_time**|**bigint**|Minimum elapsed time, in microseconds, for any completed execution of this function.|  
|**max_elapsed_time**|**bigint**|Maximum elapsed time, in microseconds, for any completed execution of this function.|  
|**total_page_server_reads**|**bigint**|Total number of page server reads performed by executions of this function since it was compiled.<br /><br /> **Applies To:** Azure SQL Database Hyperscale.|  
|**last_page_server_reads**|**bigint**|Number of page server reads performed the last time the function was executed.<br /><br /> **Applies To:** Azure SQL Database Hyperscale.|  
|**min_page_server_reads**|**bigint**|Minimum number of page server reads that this function has ever performed during a single execution.<br /><br /> **Applies To:** Azure SQL Database Hyperscale.|  
|**max_page_server_reads**|**bigint**|Maximum number of page server reads that this function has ever performed during a single execution.<br /><br /> **Applies To:** Azure SQL Database Hyperscale.|
  
## Permissions  

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## Examples  
 The following example returns information about the top ten functions identified by average elapsed time.  
  
```sql  
SELECT TOP 10 d.object_id, d.database_id, OBJECT_NAME(object_id, database_id) 'function name',   
    d.cached_time, d.last_execution_time, d.total_elapsed_time,  
    d.total_elapsed_time/d.execution_count AS [avg_elapsed_time],  
    d.last_elapsed_time, d.execution_count  
FROM sys.dm_exec_function_stats AS d  
ORDER BY [total_worker_time] DESC;  
```  
  
## See Also  
 [Execution Related Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)   
 
 [sys.dm_exec_trigger_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-trigger-stats-transact-sql.md)   
 [sys.dm_exec_procedure_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-procedure-stats-transact-sql.md)  
  
