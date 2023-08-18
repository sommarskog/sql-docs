---
title: "View the Table Definition"
description: "View the Table Definition"
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "03/21/2023"
ms.service: sql
ms.subservice: table-view-index
ms.topic: conceptual
helpviewer_keywords:
  - "showing table properties"
  - "displaying table properties"
  - "tables [SQL Server], properties"
  - "viewing table properties"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# View the Table Definition
[!INCLUDE [sqlserver2016-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi-asa-pdw.md)]

  You can display properties for a table in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)].  
    
###  <a name="Permissions"></a> Permissions  
 You can only see properties in a table if you either own the table or have been granted permissions to that table.  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
#### To show table properties in the Properties window  
  
1.  In Object Explorer, select the table for which you want to show properties.  
  
2.  Right-click the table and select **Properties** from the shortcut menu. For more information, see [Table Properties - SSMS](../../relational-databases/tables/table-properties-ssms.md).  

#### To generate the CREATE TABLE script for an existing table
  
You can script out existing objects from the Object Explorer in SSMS. For more information, see [Generate Scripts](../../ssms/scripting/generate-scripts-sql-server-management-studio.md#ScriptSingleObject).

##  <a name="TsqlProcedure"></a> Using Transact-SQL  
  
#### To show table properties  
  
1.  In **Object Explorer**, connect to an instance of [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  On the Standard bar, select **New Query**.  
  
3.  Copy and paste the following example into the query window and select **Execute**. The example executes the system stored procedure `sp_help` to return all column information for the specified object.  
  
```sql  
EXEC sp_help 'dbo.mytable';
```  

 For more information, see [sp_help](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md).
 
 By default, SSMS maps a keyboard shortcut for `sp_help` to the `Alt-F1`. Highlight the name of the object in a script you want to see, for example `dbo.mytable`, and hit `Alt-F1` to execute the previous script sample. For more information, see [SSMS keyboard shortcuts](../../ssms/sql-server-management-studio-keyboard-shortcuts.md).

 You could alternatively query the system catalog views directly to query object metadata information about tables, schema, and columns. For example:  
 
```sql
SELECT s.name as schema_name, t.name as table_name, c.* FROM sys.columns AS c
INNER JOIN sys.tables AS t ON t.object_id = c.object_id
INNER JOIN sys.schemas AS s ON s.schema_id = t.schema_id
WHERE t.name = 'mytable' AND s.name = 'dbo';
``` 

## Next Steps

* [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)    
* [sys.tables (Transact-SQL)](../../relational-databases/system-catalog-views/sys-tables-transact-sql.md)    
* [sys.schemas (Transact-SQL)](../../relational-databases/system-catalog-views/schemas-catalog-views-sys-schemas.md)     
* [Generate Scripts (SQL Server Management Studio)](../../ssms/scripting/generate-scripts-sql-server-management-studio.md)
* [SSMS keyboard shortcuts](../../ssms/sql-server-management-studio-keyboard-shortcuts.md)
