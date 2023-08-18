---
title: "sys.dm_exec_query_profiles (Transact-SQL)"
description: sys.dm_exec_query_profiles (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_exec_query_profiles_TSQL"
  - "sys.dm_exec_query_profiles_TSQL"
  - "dm_exec_query_profiles"
  - "sys.dm_exec_query_profiles"
helpviewer_keywords:
  - "sys.dm_exec_query_profiles dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: ">=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_exec_query_profiles (Transact-SQL)
[!INCLUDE[sql-asdb-asdbmi](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Monitors real time query progress while the query is in execution. For example, use this DMV to determine which part of the query is running slow. Join this DMV with other system DMVs using the columns identified in the description field. Or, join this DMV with other performance counters (such as Performance Monitor, xperf) by using the timestamp columns.  
  
## Table Returned  
The counters returned are per operator per thread. The results are dynamic and do not match the results of existing options such as `SET STATISTICS XML ON` which only create output when the query is finished.  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|session_id|**smallint**|Identifies the session in which this query runs. References dm_exec_sessions.session_id.|  
|request_id|**int**|Identifies the target request. References dm_exec_sessions.request_id.|  
|sql_handle|**varbinary(64)**|Is a token that uniquely identifies the batch or stored procedure that the query is part of. References dm_exec_query_stats.sql_handle.|  
|plan_handle|**varbinary(64)**|Is a token that uniquely identifies a query execution plan for a batch that has executed and its plan resides in the plan cache, or is currently executing. References dm_exec_query_stats.plan_handle.|  
|physical_operator_name|**nvarchar(256)**|Physical operator name.|  
|node_id|**int**|Identifies an operator node in the query tree.|  
|thread_id|**int**|Distinguishes the threads (for a parallel query) belonging to the same query operator node.|  
|task_address|**varbinary(8)**|Identifies the SQLOS task that this thread is using. References dm_os_tasks.task_address.|  
|row_count|**bigint**|Number of rows returned by the operator so far.|  
|rewind_count|**bigint**|Number of rewinds so far.|  
|rebind_count|**bigint**|Number of rebinds so far.|  
|end_of_scan_count|**bigint**|Number of end of scans so far.|  
|estimate_row_count|**bigint**|Estimated number of rows. It can be useful to compare to estimated_row_count to the actual row_count.|  
|first_active_time|**bigint**|The time, in milliseconds, when the operator was first called.|  
|last_active_time|**bigint**|The time, in milliseconds, when the operator was last called.|  
|open_time|**bigint**|Timestamp when open (in milliseconds).|  
|first_row_time|**bigint**|Timestamp when first row was opened (in milliseconds).|  
|last_row_time|**bigint**|Timestamp when last row was opened(in milliseconds).|  
|close_time|**bigint**|Timestamp when close (in milliseconds).|  
|elapsed_time_ms|**bigint**|Total elapsed time (in milliseconds) used by the target node's operations so far.|  
|cpu_time_ms|**bigint**|Total CPU time (in milliseconds) use by target node's operations so far.|  
|database_id|**smallint**|ID of the database that contains the object on which the reads and writes are being performed.|  
|object_id|**int**|The identifier for the object on which the reads and writes are being performed. References sys.objects.object_id.|  
|index_id|**int**|The index (if any) the rowset is opened against.|  
|scan_count|**bigint**|Number of table/index scans so far.|  
|logical_read_count|**bigint**|Number of logical reads so far.|  
|physical_read_count|**bigint**|Number of physical reads so far.|  
|read_ahead_count|**bigint**|Number of read-aheads so far.|  
|write_page_count|**bigint**|Number of page-writes so far due to spilling.|  
|lob_logical_read_count|**bigint**|Number of LOB logical reads so far.|  
|lob_physical_read_count|**bigint**|Number of LOB physical reads so far.|  
|lob_read_ahead_count|**bigint**|Number of LOB read-aheads so far.|  
|segment_read_count|**int**|Number of segment read-aheads so far.|  
|segment_skip_count|**int**|Number of segments skipped so far.| 
|actual_read_row_count|**bigint**|Number of rows read by an operator before the residual predicate was applied.| 
|estimated_read_row_count|**bigint**|**Applies to:** Beginning with [!INCLUDE[ssSQL15_md](../../includes/sssql16-md.md)] SP1. <br/>Number of rows estimated to be read by an operator before the residual predicate was applied.|  
  
## General Remarks  
 If the query plan node does not have any I/O, all the I/O-related counters are set to NULL.  
  
 The I/O-related counters reported by this DMV are more granular than the ones reported by `SET STATISTICS IO` in the following two ways:  
  
-   `SET STATISTICS IO` groups the counters for all I/O to a given table together. With this DMV you will get separate counters for every node in the query plan that performs I/O to the table.  
  
-   If there is a parallel scan, this DMV reports counters for each of the parallel threads working on the scan.
 
Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] SP1, the *standard query execution statistics profiling infrastructure* exists side-by-side with a *lightweight query execution statistics profiling infrastructure*. `SET STATISTICS XML ON` and `SET STATISTICS PROFILE ON` always use the *standard query execution statistics profiling infrastructure*. For `sys.dm_exec_query_profiles` to be populated, one of the query profiling infrastructures must be enabled. For more information, see [Query Profiling Infrastructure](../../relational-databases/performance/query-profiling-infrastructure.md).    

>[!NOTE]
> The query under investigation has to start **after** the query profiling infrastructure has been enabled, enabling it after the query started will not produce results in `sys.dm_exec_query_profiles`. For more information on how to enable the query profiling infrastructures, see [Query Profiling Infrastructure](../../relational-databases/performance/query-profiling-infrastructure.md).

## Permissions  

- On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and Azure SQL Managed Instance, requires `VIEW DATABASE STATE` permission and membership of the `db_owner` database role.   
- On [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)] Premium Tiers, requires the `VIEW DATABASE STATE` permission in the database. 
- On [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)] Basic, S0, and S1 service objectives, and for databases in elastic pools, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account or the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account is required. On all other SQL Database service objectives, the `VIEW DATABASE STATE` permission is required in the database.   
   
### Permissions for SQL Server 2022 and later

Requires VIEW DATABASE PERFORMANCE STATE permission on the database.

## Examples  
 Step 1: Login to a session in which you plan to run the query you will analyze with `sys.dm_exec_query_profiles`. To configure the query for profiling use `SET STATISTICS PROFILE ON`. Run your query in this same session.  
  
```sql  
--Configure query for profiling with sys.dm_exec_query_profiles  
SET STATISTICS PROFILE ON;  
GO  

--Or enable query profiling globally under SQL Server 2016 SP1 or above (not needed in SQL Server 2019)  
DBCC TRACEON (7412, -1);  
GO 
  
--Next, run your query in this session, or in any other session if query profiling has been enabled globally 
```  
  
 Step 2: Login to a second session that is different from the session in which your query is running.  
  
 The following statement summarizes the progress made by the query currently running in session 54. To do this, it calculates the total number of output rows from all threads for each node, and compares it to the estimated number of output rows for that node.  
  
```sql  
--Run this in a different session than the session in which your query is running. 
--Note that you may need to change session id 54 below with the session id you want to monitor.
SELECT node_id,physical_operator_name, SUM(row_count) row_count, 
  SUM(estimate_row_count) AS estimate_row_count, 
  CAST(SUM(row_count)*100 AS float)/SUM(estimate_row_count)  
FROM sys.dm_exec_query_profiles   
WHERE session_id=54
GROUP BY node_id,physical_operator_name  
ORDER BY node_id;  
```  
  
## See Also  
 [Dynamic Management Views and Functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Execution Related Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)  
