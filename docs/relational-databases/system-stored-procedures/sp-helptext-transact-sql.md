---
title: "sp_helptext (Transact-SQL)"
description: "sp_helptext (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "08/19/2021"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_helptext"
  - "sp_helptext_TSQL"
helpviewer_keywords:
  - "sp_helptext"
dev_langs:
  - "TSQL"
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# sp_helptext (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Displays the definition of a user-defined rule, default, unencrypted [!INCLUDE[tsql](../../includes/tsql-md.md)] stored procedure, user-defined [!INCLUDE[tsql](../../includes/tsql-md.md)] function, trigger, computed column, CHECK constraint, view, or system object such as a system stored procedure.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql  
sp_helptext [ @objname = ] 'name' [ , [ @columnname = ] computed_column_name ]  
```  
  
## Arguments  
`[ @objname = ] 'name'`
 Is the qualified or nonqualified name of a user-defined, schema-scoped object. Quotation marks are required only if a qualified object is specified. If a fully qualified name, including a database name, is provided, the database name must be the name of the current database. The object must be in the current database. *name* is **nvarchar(776)**, with no default.  
  
`[ @columnname = ] 'computed_column_name'`
 Is the name of the computed column for which to display definition information. The table that contains the column must be specified as *name*. *column_name* is **sysname**, with no default.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
  
|Column name|Data type|Description|  
|-----------------|---------------|-----------------|  
|**Text**|**nvarchar(255)**|Object definition|  
  
## Remarks  
 sp_helptext displays the definition that is used to create an object in multiple rows. Each row contains 255 characters of the [!INCLUDE[tsql](../../includes/tsql-md.md)] definition. The definition resides in the `definition` column in the [sys.sql_modules](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md) catalog view.  

> [!NOTE]
> The system stored procedure `sp_helptext` is not supported in Azure Synapse Analytics. Instead, use `OBJECT_DEFINITION` system function or `sys.sql_modules` object catalog view for equivalent results.
  
## Permissions  
 Requires membership in the **public** role. System object definitions are publicly visible. The definition of user objects is visible to the object owner or grantees that have any one of the following permissions: **ALTER**, **CONTROL**, **TAKE OWNERSHIP**, or **VIEW DEFINITION**.  
  
## Examples  
  
### A. Displaying the definition of a trigger  
 The following example displays the definition of the trigger `dEmployee` in the [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]database.  
  
```sql  
USE AdventureWorks2022;  
GO  
EXEC sp_helptext 'HumanResources.dEmployee';  
GO  
```  
  
### B. Displaying the definition of a computed column  
 The following example displays the definition of the computed column `TotalDue` on the `SalesOrderHeader` table in the [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] database.  
  
```sql  
USE AdventureWorks2022;  
GO  
sp_helptext @objname = N'AdventureWorks2022.Sales.SalesOrderHeader', @columnname = TotalDue ;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 `Text`  
  
 `---------------------------------------------------------------------`  
  
 `(isnull(([SubTotal]+[TaxAmt])+[Freight],(0)))`  
  
## See Also  
 [Database Engine Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](../../t-sql/functions/object-definition-transact-sql.md)   
 [sp_help &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-transact-sql.md)   
 [sys.sql_modules &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-sql-modules-transact-sql.md)   
 [System Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
