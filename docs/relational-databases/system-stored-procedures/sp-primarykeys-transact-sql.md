---
title: "sp_primarykeys (Transact-SQL)"
description: "sp_primarykeys (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_primarykeys_TSQL"
  - "sp_primarykeys"
helpviewer_keywords:
  - "sp_primarykeys"
dev_langs:
  - "TSQL"
---
# sp_primarykeys (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns the primary key columns, one row per key column, for the specified remote table.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_primarykeys [ @table_server = ] 'table_server'   
     [ , [ @table_name = ] 'table_name' ]   
     [ , [ @table_schema = ] 'table_schema' ]   
     [ , [ @table_catalog = ] 'table_catalog' ]  
```  
  
## Arguments  
`[ @table_server = ] 'table_server'_`
 Is the name of the linked server from which to return primary key information. *table_server* is **sysname**, with no default.  
  
`[ @table_name = ] 'table_name'`
 Is the name of the table for which to provide primary key information. *table_name*is **sysname**, with a default of NULL.  
  
`[ @table_schema = ] 'table_schema'`
 Is the table schema. *table_schema* is **sysname**, with a default of NULL. In the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] environment, this corresponds to the table owner.  
  
`[ @table_catalog = ] 'table_catalog'`
 Is the name of the catalog in which the specified *table_name* resides. In the [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] environment, this corresponds to the database name. *table_catalog* is **sysname**, with a default of NULL.  
  
## Return Code Values  
 None  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_CAT**|**sysname**|Table catalog.|  
|**TABLE_SCHEM**|**sysname**|Table schema.|  
|**TABLE_NAME**|**sysname**|Name of the table.|  
|**COLUMN_NAME**|**sysname**|Name of the column.|  
|**KEY_SEQ**|**int**|Sequence number of the column in a multicolumn primary key.|  
|**PK_NAME**|**sysname**|Primary key identifier. Returns NULL if not applicable to the data source.|  
  
## Remarks  
 **sp_primarykeys** is executed by querying the PRIMARY_KEYS rowset of the **IDBSchemaRowset** interface of the OLE DB provider corresponding to *table_server*. The *table_name*, *table_schema*, *table_catalog*, and *column* parameters are passed to this interface to restrict the rows returned.  
  
 **sp_primarykeys** returns an empty result set if the OLE DB provider of the specified linked server does not support the PRIMARY_KEYS rowset of the **IDBSchemaRowset** interface.  
  
## Permissions  
 Requires SELECT permission on the schema.  
  
## Examples  
 The following example returns primary key columns from the `LONDON1` server for the `HumanResources.JobCandidate` table in the [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database.  
  
```  
EXEC sp_primarykeys @table_server = N'LONDON1',   
   @table_name = N'JobCandidate',  
   @table_catalog = N'AdventureWorks2022',   
   @table_schema = N'HumanResources';  
```  
  
## See Also  
 [Distributed Queries Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/distributed-queries-stored-procedures-transact-sql.md)   
 [sp_catalogs &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-catalogs-transact-sql.md)   
 [sp_column_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-column-privileges-transact-sql.md)   
 [sp_foreignkeys &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-foreignkeys-transact-sql.md)   
 [sp_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-indexes-transact-sql.md)   
 [sp_linkedservers &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-linkedservers-transact-sql.md)   
 [sp_tables_ex &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-tables-ex-transact-sql.md)   
 [sp_table_privileges &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-table-privileges-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
