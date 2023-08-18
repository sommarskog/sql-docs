---
title: "sys.dm_os_memory_nodes (Transact-SQL)"
description: sys.dm_os_memory_nodes (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "02/27/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "dm_os_memory_nodes_TSQL"
  - "sys.dm_os_memory_nodes"
  - "sys.dm_os_memory_nodes_TSQL"
  - "dm_os_memory_nodes"
helpviewer_keywords:
  - "sys.dm_os_memory_nodes dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sys.dm_os_memory_nodes (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Allocations that are internal to [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory manager. Tracking the difference between process memory counters from **sys.dm_os_process_memory** and internal counters can indicate memory use from external components in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory space.  
  
 Nodes are created per physical NUMA memory nodes. These might be different from the CPU nodes in **sys.dm_os_nodes**.  
  
 No allocations done directly through Windows memory allocations routines are tracked. The following table provides information about memory allocations done only by using [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] memory manager interfaces.  
  
> [!NOTE]  
>  To call this from [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use the name **sys.dm_pdw_nodes_os_memory_nodes**. [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**memory_node_id**|**smallint**|Specifies the ID of the memory node. Related to **memory_node_id** of **sys.dm_os_memory_clerks**. Not nullable.|  
|**virtual_address_space_reserved_kb**|**bigint**|Indicates the number of virtual address reservations, in kilobytes (KB), which are neither committed nor mapped to physical pages. Not nullable.|  
|**virtual_address_space_committed_kb**|**bigint**|Specifies the amount of virtual address, in KB, that has been committed or mapped to physical pages. Not nullable.|  
|**locked_page_allocations_kb**|**bigint**|Specifies the amount of physical memory, in KB, that has been locked by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Not nullable.|  
|**single_pages_kb**|**bigint**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] through [!INCLUDE[sql2008r2](../../includes/sql2008r2-md.md)].<br /><br /> Amount of committed memory, in KB, that is allocated by using the single page allocator by threads running on this node. This memory is allocated from the buffer pool. This value indicates the node where allocations request occurred, not the physical location where the allocation request was satisfied.|  
|**pages_kb**|**bigint**|**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.<br /><br /> Specifies the amount of committed memory, in KB, which is allocated from this NUMA node by Memory Manager Page Allocator. Not nullable.|  
|**multi_pages_kb**|**bigint**|**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] through [!INCLUDE[sql2008r2](../../includes/sql2008r2-md.md)].<br /><br /> Amount of committed memory, in KB, that is allocated by using the multipage allocator by threads running on this node. This memory is from outside the buffer pool. This value indicates the node where the allocation requests occurred, not the physical location where the allocation request was satisfied.|  
|**shared_memory_reserved_kb**|**bigint**|Specifies the amount of shared memory, in KB, that has been reserved from this node. Not nullable.|  
|**shared_memory_committed_kb**|**bigint**|Specifies the amount of shared memory, in KB, that has been committed on this node. Not nullable.|  
|**cpu_affinity_mask**|**bigint**|**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.<br /><br /> Internal use only. Not nullable.|  
|**online_scheduler_mask**|**bigint**|**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.<br /><br /> Internal use only. Not nullable.|  
|**processor_group**|**smallint**|**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.<br /><br /> Internal use only. Not nullable.|  
|**foreign_committed_kb**|**bigint**|**Applies to**: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and later.<br /><br /> Specifies the amount of committed memory, in KB, from other memory nodes. Not nullable.|  
|**target_kb** |**bigint** |**Applies to**: [!INCLUDE[ssSQL15_md](../../includes/sssql16-md.md)] and later, [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)].<br /><br /> Specifies the memory goal for the memory node, in KB. |   
|**pdw_node_id**|**int**|**Applies to**: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> The identifier for the node that this distribution is on.|  
  
## Permissions

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   

### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## See also  
  [SQL Server Operating System Related Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
