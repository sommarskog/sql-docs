---
title: "SQL Server, Memory Manager object"
description: Learn about the Memory Manager object, which provides counters to monitor overall server memory usage in SQL Server.
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "07/13/2021"
ms.service: sql
ms.subservice: performance
ms.topic: conceptual
helpviewer_keywords:
  - "SQLServer:Memory Manager"
  - "Memory Manager object"
---
# SQL Server, Memory Manager object
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  The **Memory Manager** object in Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provides counters to monitor overall server memory usage. Monitoring overall server memory usage to gauge user activity and resource usage can help you to identify performance bottlenecks. Monitoring the memory used by an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can help determine:  
  
-   If bottlenecks exist from inadequate physical memory for storing frequently accessed data in cache. If memory is inadequate, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] must retrieve the data from disk.  
  
-   If query performance can be improved by adding more memory or by making more memory available to the data cache or [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] internal structures.  
  
## Memory Manager Counters  
 This table describes the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Memory Manager** counters.  
  
|SQL Server Memory Manager counters|Description|  
|----------------------------------------|-----------------|  
|**Connection Memory (KB)**|Specifies the total amount of dynamic memory the server is using for maintaining connections.|  
|**Database Cache Memory (KB)**|Specifies the amount of memory the server is currently using for the database pages cache.|  
|**External benefit of memory**| An internal estimation of the performance benefit from adding memory to a specific cache. It is used by the engine to balance memory usage between cache and is useful to support when troubleshooting cases with unexpected cache growth. The value is presented as an integer based on an internal calculation. | 
|**Free Memory (KB)**|Specifies the amount of committed memory currently not used by the server.|  
|**Granted Workspace Memory (KB)**|Specifies the total amount of memory currently granted to executing processes, such as hash, sort, bulk copy, and index creation operations.|  
|**Lock Blocks**|Specifies the current number of lock blocks in use on the server (refreshed periodically). A lock block represents an individual locked resource, such as a table, page, or row.|  
|**Lock Blocks Allocated**|Specifies the current number of allocated lock blocks. At server startup, the number of allocated lock blocks plus the number of allocated lock owner blocks depends on the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** configuration option. If more lock blocks are needed, the value increases.|  
|**Lock Memory (KB)**|Specifies the total amount of dynamic memory the server is using for locks.|  
|**Lock Owner Blocks**|Specifies the number of lock owner blocks currently in use on the server (refreshed periodically). A lock owner block represents the ownership of a lock on an object by an individual thread. Therefore, if three threads each have a shared (S) lock on a page, there will be three lock owner blocks.|  
|**Lock Owner Blocks Allocated**|Specifies the current number of allocated lock owner blocks. At server startup, the number of allocated lock owner blocks and the number of allocated lock blocks depend on the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Locks** configuration option. If more lock owner blocks are needed, the value increases dynamically.|  
|**Log Pool Memory (KB)**|Total amount of dynamic memory the server is using for Log Pool.| 
|**Maximum Workspace Memory (KB)**|Indicates the maximum amount of memory available for executing processes, such as hash, sort, bulk copy, and index creation operations.|  
|**Memory Grants Outstanding**|Specifies the total number of processes that have successfully acquired a workspace memory grant.|  
|**Memory Grants Pending**|Specifies the total number of processes waiting for a workspace memory grant.|  
|**Optimizer Memory (KB)**|Specifies the total amount of dynamic memory the server is using for query optimization.|  
|**Reserved Server Memory (KB)**|Indicates the amount of memory the server has reserved for future usage. This counter shows the current unused amount of memory initially granted that is shown in **Granted Workspace Memory (KB)**.|  
|**SQL Cache Memory (KB)**|Specifies the total amount of dynamic memory the server is using for the dynamic SQL cache.|  
|**Stolen Server Memory (KB)**|Specifies the amount of memory the server is using for purposes other than database pages.|  
|**Target Server Memory (KB)**|Indicates the ideal amount of memory the server can consume.|  
|**Total Server Memory (KB)**|Specifies the amount of memory the server has committed using the memory manager.|  
 
  
## Example

You begin to explore the query performance counters in this object using this T-SQL query on the [sys.dm_os_performance_counters](../system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md) dynamic management view:

```sql
SELECT * FROM sys.dm_os_performance_counters
WHERE object_name LIKE '%Memory Manager%';
```  

## See also  
 [Monitor Resource Usage &#40;System Monitor&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [SQL Server, Buffer Manager Object](../../relational-databases/performance-monitor/sql-server-buffer-manager-object.md)   
 [sys.dm_os_performance_counters (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-performance-counters-transact-sql.md)  
  
