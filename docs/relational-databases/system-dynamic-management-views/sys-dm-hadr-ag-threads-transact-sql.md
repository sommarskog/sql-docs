---
title: "sys.dm_hadr_ag_threads (Transact-SQL)"
description: sys.dm_hadr_ag_threads (Transact-SQL)
author: kfarlee
ms.author: kfarlee
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "language-reference"
f1_keywords:
  - "sys.dm_hadr_ag_threads_TSQL"
  - "sys.dm_hadr_ag_threads"
  - "dm_hadr_ag_threads_TSQL"
  - "dm_hadr_ag_threads"
helpviewer_keywords:
  - "Availability Groups [SQL Server], monitoring"
  - "Availability Groups [SQL Server], WSFC clusters"
  - "sys.dm_hadr_ag_threads catalog view"
dev_langs:
  - "TSQL"
---
# sys.dm_hadr_ag_threads (Transact-SQL)

The HADR thread telemetry DMVs (**sys.dm_hadr_ag_threads** and [sys.dm_hadr_db_threads](../../relational-databases/system-dynamic-management-views/sys-dm-hadr-db-threads-transact-sql.md)) allow users to quickly gain insight into thread usage by availability group and by high availability database. Understanding this thread usage is an important benchmark for tuning availability groups.

This DMV reports on thread usage at the availability group level.

|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**group_id**|**uniqueidentifier**|Identifier of the availability group.|
|**name**|**nvarchar(128)**|Name of the availability group.|
|**num_databases**|**int**|Number of databases in the availability group.|
|**num_capture_threads**|**int**|Number of log capture threads used by all databases in this availability group.|
|**num_redo_threads**|**int**|Number of redo threads used by all databases in this availability group.|
|**num_parallel_redo_threads**|**int**|Number of parallel redo threads used by all databases in this availability group.|
|**num_hadr_threads**|**int**|Number of all always on threads used by all databases in this availability group.|

## Permissions  

 Requires VIEW SERVER STATE permission on the server.  
  
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## See also  

 [Always On Availability Groups Dynamic Management Views and Functions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)   
 [Always On Availability Groups Catalog Views &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/always-on-availability-groups-catalog-views-transact-sql.md)   
 [Monitor Availability Groups &#40;Transact-SQL&#41;](../../database-engine/availability-groups/windows/monitor-availability-groups-transact-sql.md)   
 [Always On Availability Groups &#40;SQL Server&#41;](../../database-engine/availability-groups/windows/always-on-availability-groups-sql-server.md)  
  
