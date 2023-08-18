---
title: "sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)"
description: sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_db_column_store_row_group_operational_stats (Transact-SQL)

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

  Returns current row-level I/O, locking, and access method activity for compressed rowgroups in a columnstore index. Use **sys.dm_db_column_store_row_group_operational_stats** to track the length of time a user query must wait to read or write to a compressed rowgroup or partition of a columnstore index, and identify rowgroups that are encountering significant I/O activity or hot spots.  
  
 In-memory columnstore indexes do not appear in this DMV.  
 
 
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|ID of the table with the columnstore index.|  
|**index_id**|**int**|ID of the columnstore index.|  
|**partition_number**|**int**|1-based partition number within the index or heap.|  
|**row_group_id**|**int**|ID of the rowgroup in the columnstore index. This is unique within a partition.|  
|**scan_count**|**int**|Number of scans through the rowgroup since the last SQL restart.|  
|**delete_buffer_scan_count**|**int**|Number of times the delete buffer was used to determine deleted rows in this rowgroup. This includes accessing the in-memory hashtable and the underlying B-tree.|  
|**index_scan_count**|**int**|Number of times the columnstore index partition was scanned. This is the same for all rowgroups in the partition.|  
|**rowgroup_lock_count**|**bigint**|Cumulative count of lock requests for this rowgroup since the last SQL restart.|  
|**rowgroup_lock_wait_count**|**bigint**|Cumulative number of times the database engine waited on this rowgroup lock since the last SQL restart.|  
|**rowgroup_lock_wait_in_ms**|**bigint**|Cumulative number of milliseconds the database engine waited on this rowgroup lock since the last SQL restart.|  

[!INCLUDE [sql-b-tree](../../includes/sql-b-tree.md)]

## Permissions  
 Requires the following permissions:  
  
-   CONTROL permission on the table specified by object_id.  
  
-   VIEW DATABASE STATE permission to return information about all objects within the database, by using the object wildcard @*object_id* = NULL  
  
 Granting VIEW DATABASE STATE allows all objects in the database to be returned, regardless of any CONTROL permissions denied on specific objects.  
  
 Denying VIEW DATABASE STATE disallows all objects in the database to be returned, regardless of any CONTROL permissions granted on specific objects. Also, when the database wildcard @*database_id*=NULL is specified, the database is omitted.  
  
 For more information, see [Dynamic Management Views and Functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md).  
  
### Permissions for SQL Server 2022 and later

Requires VIEW DATABASE PERFORMANCE STATE permission on the database.

## See Also  
 [Dynamic Management Views and Functions &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Index Related Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [Monitor and Tune for Performance](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_os_latch_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  

