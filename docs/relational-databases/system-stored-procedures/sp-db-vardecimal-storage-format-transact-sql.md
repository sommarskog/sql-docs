---
title: "sp_db_vardecimal_storage_format (Transact-SQL)"
description: "sp_db_vardecimal_storage_format (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: system-objects
ms.topic: "reference"
f1_keywords:
  - "sp_db_vardecimal_storage_format"
  - "sp_db_vardecimal_storage_format_TSQL"
helpviewer_keywords:
  - "sp_db_vardecimal_storage_format"
  - "decimal data type, compressing"
  - "compressing decimal data"
  - "numeric data type, compressing"
  - "database compression [SQL Server]"
  - "table compression [SQL Server]"
dev_langs:
  - "TSQL"
---
# sp_db_vardecimal_storage_format (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Returns the current vardecimal storage format state of a database or enables a database for vardecimal storage format.  Starting with [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)], user databases are always enabled. Enabling databases for the vardecimal storage format is only necessary in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
> [!NOTE]  
> [!INCLUDE[sssql19-md](../../includes/sssql19-md.md)] supports the vardecimal storage format; however, because row-level compression achieves the same goals, the vardecimal storage format is deprecated. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]
  
> [!IMPORTANT]  
> Changing the vardecimal storage format state of a database can affect backup and recovery, database mirroring, sp_attach_db, log shipping, and replication.  
  
## Syntax  
  
```syntaxsql  
sp_db_vardecimal_storage_format [ [ @dbname = ] 'database_name']   
    [ , [ @vardecimal_storage_format = ] { 'ON' | 'OFF' } ]   
[;]  
```  
  
## Arguments  
 [ @dbname= ] '*database_name*'  
 Is the name of the database for which the storage format is to be changed. *database_name* is **sysname**, with no default. If the database name is omitted, the vardecimal storage format status of all the databases in the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] are returned.  
  
 [ @vardecimal_storage_format= ] {'ON'|'OFF'}  
 Specifies whether the vardecimal storage format is enabled. @vardecimal_storage_format can be ON or OFF. The parameter is **varchar(3)**, with no default. If a database name is provided but @vardecimal_storage_format is omitted, the current setting of the specified database is returned. 
 
 > [!IMPORTANT]
 > This argument has no effect on [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] or later versions.  
  
## Return Code Values  
 0 (success) or 1 (failure)  
  
## Result Sets  
 If the database storage format cannot be changed, sp_db_vardecimal_storage_format returns an error. If the database is already in the specified state, the stored procedure has no effect.  
  
 If the @vardecimal_storage_format argument is not provided, returns the columns Database Name and the Vardecimal State.  
  
## Remarks  
 sp_db_vardecimal_storage_format returns the vardecimal state but cannot change the vardecimal state.  
  
 sp_db_vardecimal_storage_format will fail in the following circumstances:  
  
-   There are active users in the database.  
  
-   The database is enabled for mirroring.  
  
-   The edition of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] does not support vardecimal storage format.  
  
 To change the vardecimal storage format state to OFF, a database must be set to simple recovery mode. When a database is set to simple recovery mode, the log chain is broken. Perform a full database backup after you set the vardecimal storage format state to OFF.  
  
 Changing the state to OFF will fail if there are tables using vardecimal database compression. To change the storage format of a table, use [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). To determine which tables in a database are using vardecimal storage format, use the `OBJECTPROPERTY` function and search for the `TableHasVarDecimalStorageFormat` property, as shown in the following example.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT name, object_id, type_desc  
FROM sys.objects   
 WHERE OBJECTPROPERTY(object_id,   
   N'TableHasVarDecimalStorageFormat') = 1 ;  
GO  
```  
  
## Examples  
 The following code enables compression in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database, confirms the state, and then compresses decimal and numeric columns in the `Sales.SalesOrderDetail` table.  
  
```sql  
USE master ;  
GO  
  
EXEC sp_db_vardecimal_storage_format 'AdventureWorks2022', 'ON' ;  
GO  
  
-- Check the vardecimal storage format state for  
-- all databases in the instance.  
EXEC sp_db_vardecimal_storage_format ;  
GO  
  
USE AdventureWorks2022;  
GO  
  
EXEC sp_tableoption 'Sales.SalesOrderDetail', 'vardecimal storage format', 1 ;  
GO  
```  
  
## See Also  
 [Database Engine Stored Procedures &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
