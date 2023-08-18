---
title: "sys.dm_os_buffer_descriptors (Transact-SQL)"
description: sys.dm_os_buffer_descriptors (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.date: "06/19/2023"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sys.dm_os_buffer_descriptors_TSQL"
  - "dm_os_buffer_descriptors_TSQL"
  - "sys.dm_os_buffer_descriptors"
  - "dm_os_buffer_descriptors"
helpviewer_keywords:
  - "sys.dm_os_buffer_descriptors dynamic management view"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||>=aps-pdw-2016||=azure-sqldw-latest"
---
# sys.dm_os_buffer_descriptors (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Returns information about all the data pages that are currently in the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] buffer pool. The output of this view can be used to determine the distribution of database pages in the buffer pool according to database, object, or type. In [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)], this dynamic management view also returns information about the data pages in the buffer pool extension file. For more information, see [Buffer Pool Extension](../../database-engine/configure-windows/buffer-pool-extension.md).  
  
 When a data page is read from disk, the page is copied into the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] buffer pool and cached for reuse. Each cached data page has one buffer descriptor. Buffer descriptors uniquely identify each data page that is currently cached in an instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sys.dm_os_buffer_descriptors returns cached pages for all user and system databases. This includes pages that are associated with the Resource database.  
  
> [!NOTE]  
> To call this from [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] or [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use the name **sys.dm_pdw_nodes_os_buffer_descriptors**. [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]  

|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|ID of database associated with the page in the buffer pool. Is nullable. <br /><br />In [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], the values are unique within a single database or an elastic pool, but not within a logical server.|  
|file_id|**int**|ID of the file that stores the persisted image of the page. Is nullable.|  
|page_id|**int**|ID of the page within the file. Is nullable.|  
|page_level|**int**|Index level of the page. Is nullable.|  
|allocation_unit_id|**bigint**|ID of the allocation unit of the page. This value can be used to join sys.allocation_units. Is nullable.|  
|page_type|**nvarchar(60)**|Type of the page, such as: Data page or Index page. Is nullable.|  
|row_count|**int**|Number of rows on the page. Is nullable.|  
|free_space_in_bytes|**int**|Amount of available free space, in bytes, on the page. Is nullable.|  
|is_modified|**bit**|1 = Page has been modified after it was read from the disk. Is nullable.|  
|numa_node|**int**|Nonuniform Memory Access node for the buffer. Is nullable.|  
|read_microsec|**bigint**|The actual time (in microseconds) required to read the page into the buffer. This number is reset when the buffer is reused. Is nullable.| 
|is_in_bpool_extension|**bit**|1 = Page is in buffer pool extension. Is nullable.| 
|pdw_node_id|**int**|**Applies to**: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> The identifier for the node that this distribution is on.| 
  
## Permissions  

On [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] and SQL Managed Instance, requires `VIEW SERVER STATE` permission.

On SQL Database **Basic**, **S0**, and **S1** service objectives, and for databases in **elastic pools**, the [server admin](/azure/azure-sql/database/logins-create-manage#existing-logins-and-user-accounts-after-creating-a-new-database) account, the [Azure Active Directory admin](/azure/azure-sql/database/authentication-aad-overview#administrator-structure) account, or membership in the `##MS_ServerStateReader##` [server role](/azure/azure-sql/database/security-server-roles) is required. On all other SQL Database service objectives, either the `VIEW DATABASE STATE` permission on the database, or membership in the `##MS_ServerStateReader##` server role is required.   
   
### Permissions for SQL Server 2022 and later

Requires VIEW SERVER PERFORMANCE STATE permission on the server.

## Remarks  
 sys.dm_os_buffer_descriptors returns pages that are being used by the Resource database. sys.dm_os_buffer_descriptors does not return information about free or stolen pages, or about pages that had errors when they were read.  
  
|From|To|On|Relationship|  
|----------|--------|--------|------------------|  
|sys.dm_os_buffer_descriptors|sys.databases|database_id|many-to-one|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.allocation_units|allocation_unit_id|many-to-one|  
|sys.dm_os_buffer_descriptors|\<userdb>.sys.database_files|file_id|many-to-one|  
|sys.dm_os_buffer_descriptors|sys.dm_os_buffer_pool_extension_configuration|file_id|many-to-one|  
  
## Examples  
  
### A. Returning cached page count for each database  
 The following example returns the count of pages loaded for each database.  
  
```  
SELECT COUNT(*)AS cached_pages_count  
    ,CASE database_id   
        WHEN 32767 THEN 'ResourceDb'   
        ELSE db_name(database_id)   
        END AS database_name  
FROM sys.dm_os_buffer_descriptors  
GROUP BY DB_NAME(database_id) ,database_id  
ORDER BY cached_pages_count DESC;  
```  
  
### B. Returning cached page count for each object in the current database  
 The following example returns the count of pages loaded for each object in the current database.  
  
```  
SELECT COUNT(*)AS cached_pages_count   
    ,name ,index_id   
FROM sys.dm_os_buffer_descriptors AS bd   
    INNER JOIN   
    (  
        SELECT object_name(object_id) AS name   
            ,index_id ,allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.hobt_id   
                    AND (au.type = 1 OR au.type = 3)  
        UNION ALL  
        SELECT object_name(object_id) AS name     
            ,index_id, allocation_unit_id  
        FROM sys.allocation_units AS au  
            INNER JOIN sys.partitions AS p   
                ON au.container_id = p.partition_id   
                    AND au.type = 2  
    ) AS obj   
        ON bd.allocation_unit_id = obj.allocation_unit_id  
WHERE database_id = DB_ID()  
GROUP BY name, index_id   
ORDER BY cached_pages_count DESC;  
```  
  
## See also  
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 
 [SQL Server Operating System Related Dynamic Management Views &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [Resource Database](../../relational-databases/databases/resource-database.md)   
 [sys.dm_os_buffer_pool_extension_configuration &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-pool-extension-configuration-transact-sql.md)  
  
