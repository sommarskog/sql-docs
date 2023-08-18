---
title: "Modify an Index"
description: Modify an Index
author: MikeRayMSFT
ms.author: mikeray
ms.date: "02/17/2017"
ms.service: sql
ms.subservice: table-view-index
ms.topic: conceptual
helpviewer_keywords:
  - "indexes [SQL Server], modifying"
  - "modifying indexes"
  - "index changes [SQL Server]"
monikerRange: "=azuresqldb-current||>=sql-server-2016"
---
# Modify an Index
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  This topic describes how to modify an index in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)] by using [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] or [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
> [!IMPORTANT]  
>  Indexes created as the result of a PRIMARY KEY or UNIQUE constraint cannot be modified by using this method. Instead, the constraint must be modified.  
  
 **In This Topic**  
  
-   **To modify an index, using:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> Using SQL Server Management Studio  
  
#### To modify an index  
  
1.  In Object Explorer, connect to an instance of the [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] and then expand that instance.  
  
2.  Expand **Databases**, expand the database in which the table belongs, and then expand **Tables**.  
  
3.  Expand the table in which the index belongs and then expand **Indexes**.  
  
4.  Right-click the index that you want to modify and then click **Properties**.  
  
5.  In the **Index Properties** dialog box, make the desired changes. For example, you can add or remove a column from the index key, or change the setting of an index option.  
  
#### To modify index columns  
  
1.  To add, remove, or change the position of an index column, select the **General** page from the **Index Properties** dialog box.  
  
##  <a name="TsqlProcedure"></a> Using Transact-SQL  
  
#### To modify an index  
  
The following example drops and re-creates an existing index on the `ProductID` column of the `Production.WorkOrder` table in the AdventureWorks database by using the `DROP_EXISTING` option. The options `FILLFACTOR` and `PAD_INDEX` are also set.  
  
[!code-sql[IndexDDL#CreateIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_1.sql)]  
  
The following example uses ALTER INDEX to set several options on the index `AK_SalesOrderHeader_SalesOrderNumber`.  
  
[!code-sql[IndexDDL#AlterIndex4](../../relational-databases/indexes/codesnippet/tsql/modify-an-index_2.sql)]  
  
#### To modify index columns  
  
1.  To add, remove, or change the position of an index column, you must drop and recreate the index.  
  
## See Also  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [INDEXPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/indexproperty-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [Set Index Options](../../relational-databases/indexes/set-index-options.md)   
 [Rename Indexes](../../relational-databases/indexes/rename-indexes.md)  
  
  
