---
title: "sys.pdw_database_mappings (Transact-SQL)"
description: sys.pdw_database_mappings (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "10/17/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016"
---
# sys.pdw_database_mappings (Transact-SQL)
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  Maps the **database_id**s of databases to the physical name used on Compute nodes, and provides the **principal id** of the database owner on the system. Join **sys.pdw_database_mappings** to **sys.databases** and **sys.pdw_nodes_pdw_physical_databases**.  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|physical_name|**nvarchar(36)**|The physical name for the database on the Compute nodes.<br /><br /> **physical_name** and **database_id** form the key for this view.||  
|database_id|**int**|The object ID for the database. See [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md).<br /><br /> **physical_name** and **database_id** form the key for this view.||  
  
## Examples: [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 The following example joins sys.pdw_database_mappings to other system tables to show how databases are mapped.  
  
```  
SELECT DB.database_id, DB.name, Map.*, Phys.*   
FROM sys.databases AS DB  
JOIN sys.pdw_database_mappings AS Map  
    ON DB.database_id = Map.database_id  
JOIN sys.pdw_nodes_pdw_physical_databases AS Phys  
    ON Map.physical_name = Phys.physical_name  
ORDER BY DB.database_id, Phys.pdw_node_id;  
```  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Catalog Views](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.pdw_index_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-index-mappings-transact-sql.md)   
 [sys.pdw_table_mappings &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-table-mappings-transact-sql.md)   
 [sys.pdw_nodes_pdw_physical_databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-nodes-pdw-physical-databases-transact-sql.md)  
  
  

