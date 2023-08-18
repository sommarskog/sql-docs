---
title: "sys.pdw_nodes_columns (Transact-SQL)"
description: sys.pdw_nodes_columns (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: data-warehouse
ms.topic: "reference"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azure-sqldw-latest"
---
# sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Shows columns for user-defined tables and user-defined views.  
  
|Column Name|Data Type|Description|Range|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|ID of the object to which this column belongs.||  
|name|**sysname**|Name of the column. Unique in object.||  
|column_id|**int**|ID of the column. Unique in object.||  
|system_type_id|**tinyint**|ID of the system type of the column.||  
|user_type_id|**int**|ID of the type of the column as defined by the user.||  
|max_length|**smallint**|Maximum length (in bytes) of the column.|Includes -1 (not valid) for unsupported column types.|  
|precision|**tinyint**|Precision of the column if numeric-based; otherwise, 0.||  
|scale|**tinyint**|Scale of column if numeric-based; otherwise, 0.||  
|collation_name|**sysname**|Name of the collation of the column if character-based; otherwise, NULL.||  
|is_nullable|**bit**|1 = Column is nullable.||  
|is_ansi_padded|**bit**|1 = Column uses ANSI_PADDING ON behavior if character, binary, or variant.|Always 0.|  
|is_rowguidcol|**bit**|1 = Column is a declared ROWGUIDCOL.|Always 0.|  
|is_identity|**bit**|1 = Column has identity values.|Always 0.|  
|is_computed|**bit**|1 = Column is a computed column.|Always 0.|  
|is_filestream|**bit**|1 = Column is a FILESTREAM column.|Always 0.|  
|is_replicated|**bit**|1 = Column is replicated.|Always 0.|  
|is_non_sql_subscribed|**bit**|1 = Column has a non-SQL subscriber.|Always 0.|  
|is_merge_published|**bit**|1 = Column is merge-published.|Always 0.|  
|is_dts_replicated|**bit**|1 = Column is replicated by using SSIS.|Always 0.|  
|is_xml_document|**bit**|1 = Content is a complete XML document.|Always 0.|  
|xml_collection_id|**int**|0 = No XML schema collection.|Always 0.|  
|default_object_id|**int**|ID of the default object; 0 = No default.|Always 0.|  
|rule_object_id|**int**|ID of the stand-alone rule bound to the column. <br />0 = No stand-alone rule.|Always 0.|  
|is_sparse|**bit**|1 = Column is a sparse column.|Always 0.|  
|is_column_set|**bit**|1 = Column is a column set.|Always 0.|  
|pdw_node_id|**int**|Unique identifier of a [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] node.|NOT NULL|  
  
## Permissions  
 Requires CONTROL SERVER permission.  
  
## See Also  
 [Azure Synapse Analytics and Parallel Data Warehouse Catalog Views](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
