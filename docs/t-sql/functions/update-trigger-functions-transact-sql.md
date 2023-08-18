---
title: "UPDATE() (Transact-SQL)"
description: "UPDATE - Trigger Functions (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "03/15/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "UPDATE()_TSQL"
  - "UPDATE()"
helpviewer_keywords:
  - "INSERT statement [SQL Server], UPDATE function"
  - "testing column updates"
  - "UPDATE function"
  - "UPDATE() function"
  - "detecting changes"
  - "columns [SQL Server], change detection"
  - "UPDATE statement [SQL Server], UPDATE function"
  - "verifying column updates"
  - "checking column updates"
dev_langs:
  - "TSQL"
---
# UPDATE - Trigger Functions (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

  Returns a Boolean value that indicates whether an INSERT or UPDATE attempt was made on a specified column of a table or view. UPDATE() is used anywhere inside the body of a [!INCLUDE[tsql](../../includes/tsql-md.md)] INSERT or UPDATE trigger to test whether the trigger should execute certain actions.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
UPDATE ( column )   
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *column*  
 Is the name of the column to test for either an INSERT or UPDATE action. Because the table name is specified in the ON clause of the trigger, do not include the table name before the column name. The column can be of any [data type](../../t-sql/data-types/data-types-transact-sql.md) supported by [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. However, computed columns cannot be used in this context.  
  
## Return Types  
 Boolean  
  
## Remarks  
 UPDATE() returns TRUE regardless of whether an INSERT or UPDATE attempt is successful.  
  
 To test for an INSERT or UPDATE action for more than one column, specify a separate UPDATE(*column*) clause following the first one. Multiple columns can also be tested for INSERT or UPDATE actions by using COLUMNS_UPDATED. This returns a bit pattern that indicates which columns were inserted or updated.  
  
 IF UPDATE returns the TRUE value in INSERT actions because the columns have either explicit values or implicit (NULL) values inserted.  
  
> [!NOTE]  
>  The IF UPDATE(*column*) clause functions the same as an IF, IF...ELSE, or WHILE clause and can use the BEGIN...END block. For more information, see [Control-of-Flow Language &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md).  
  
 UPDATE(*column*) can be used anywhere inside the body of a [!INCLUDE[tsql](../../includes/tsql-md.md)] trigger.  
 
If a trigger applies to a column, the `UPDATED` value will return as `true` or `1`, even if the column value remains unchanged. This is by-design, and the trigger should implement business logic that determines if the insert/update/delete operation is permissible or not. 
  
## Examples  
 The following example creates a trigger that prints a message to the client when anyone tries to update the `StateProvinceID` or `PostalCode` columns of the `Address` table.  
  
```sql  
USE AdventureWorks2022;  
GO  
IF EXISTS (SELECT name FROM sys.objects  
      WHERE name = 'reminder' AND type = 'TR')  
   DROP TRIGGER Person.reminder;  
GO  
CREATE TRIGGER reminder  
ON Person.Address  
AFTER UPDATE   
AS   
IF ( UPDATE (StateProvinceID) OR UPDATE (PostalCode) )  
BEGIN  
RAISERROR (50009, 16, 10)  
END;  
GO  
-- Test the trigger.  
UPDATE Person.Address  
SET PostalCode = 99999  
WHERE PostalCode = '12345';  
GO  
```  
  
## See Also  
 [COLUMNS_UPDATED &#40;Transact-SQL&#41;](../../t-sql/functions/columns-updated-transact-sql.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)  
  
  
