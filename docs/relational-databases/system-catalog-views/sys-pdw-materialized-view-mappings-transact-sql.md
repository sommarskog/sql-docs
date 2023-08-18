---
title: "sys.pdw_materialized_view_mappings (Transact-SQL)"
description: sys.pdw_materialized_view_mappings (Transact-SQL)
author: XiaoyuMSFT
ms.author: xiaoyul
ms.date: "07/03/2019"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: "=azure-sqldw-latest"
---
# sys.pdw_materialized_view_mappings (Transact-SQL)  

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

Ties the materialized view to internal object names by object_id.

The columns physical_name and object_id form the key for this catalog view.
  
|Column Name|Data Type|Description|  
|-----------------|---------------|-----------------|  
|physical_name |**nvarchar(36)**|The physical name for the materialized view.|  
|object_id  |**int**|The object ID for the materialized view. See [sys.objects (Transact-SQL)](./sys-objects-transact-sql.md?view=azure-sqldw-latest&preserve-view=true).| 

## Permissions

Requires VIEW DATABASE STATE permission.
  
## See also

[Performance tuning with Materialized View](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[CREATE MATERIALIZED VIEW AS SELECT &#40;Transact-SQL&#41;](../../t-sql/statements/create-materialized-view-as-select-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/alter-materialized-view-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[EXPLAIN &#40;Transact-SQL&#41;](../../t-sql/queries/explain-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-column-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](./sys-pdw-materialized-view-distribution-properties-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql.md?view=azure-sqldw-latest&preserve-view=true)   
[Azure Synapse Analytics and Parallel Data Warehouse Catalog Views](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[System views supported in Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[T-SQL statements supported in Azure Synapse Analytics](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
