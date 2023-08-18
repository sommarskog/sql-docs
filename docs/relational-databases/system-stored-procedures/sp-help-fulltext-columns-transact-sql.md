---
title: "sp_help_fulltext_columns (Transact-SQL)"
description: "sp_help_fulltext_columns (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_help_fulltext_columns"
  - "sp_help_fulltext_columns_TSQL"
helpviewer_keywords:
  - "sp_help_fulltext_columns"
dev_langs:
  - "TSQL"
---
# sp_help_fulltext_columns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns the columns designated for full-text indexing.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use the [sys.fulltext_index_columns](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md) catalog view instead.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```  
  
sp_help_fulltext_columns [ [ @table_name = ] 'table_name' ] ]   
     [ , [ @column_name = ] 'column_name' ]  
```  
  
## Arguments  
`[ @table_name = ] 'table\_name'`
 Is the one- or two-part table name for which full-text index information is requested. *table_name* is **nvarchar(517)**, with a default value of NULL. If *table_name* is omitted, full-text index column information is retrieved for every full-text indexed table.  
  
`[ @column_name = ] 'column\_name'`
 Is the name of the column for which full-text index metadata is requested. *column_name* is **sysname**, with a default value of NULL. If *column_name* is omitted or is NULL, full-text column information is returned for every full-text indexed column for *table_name*. If *table_name* is also omitted or is NULL, full-text index column information is returned for every full-text indexed column for all tables in the database.  
  
## Return Code Values  
 0 (success) or (1) failure  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**TABLE_OWNER**|**sysname**|Table owner. This is the name of the database user that created the table.|  
|**TABLE_ID**|**int**|ID of the table.|  
|**TABLE_NAME**|**sysname**|Name of the table.|  
|**FULLTEXT_COLUMN_NAME**|**sysname**|Column in a full-text indexed table that is designated for indexing.|  
|**FULLTEXT_COLID**|**int**|Column ID of the full-text indexed column.|  
|**FULLTEXT_BLOBTP_COLNAME**|**sysname**|Column in a full-text indexed table that specifies the document type of the full-text indexed column. This value is only applicable when the full-text indexed column is a **varbinary(max)** or **image** column.|  
|**FULLTEXT_BLOBTP_COLID**|**int**|Column ID of the document type column. This value is only applicable when the full-text indexed column is a **varbinary(max)** or **image** column.|  
|**FULLTEXT_LANGUAGE**|**sysname**|Language used for the full-text search of the column.|  
  
## Permissions  
 Execute permissions default to members of the **public** role.  
  
## Examples  
 The following example returns information about the columns that have been designated for full-text indexing in the `Document` table.  
  
```  
USE AdventureWorks2022;  
GO  
EXEC sp_help_fulltext_columns 'Production.Document';  
GO  
```  
  
## See Also  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [sp_fulltext_column &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-fulltext-column-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
