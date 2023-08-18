---
title: "CLOSE (Transact-SQL)"
description: "CLOSE (Transact-SQL)"
author: rwestMSFT
ms.author: randolphwest
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "CLOSE_TSQL"
  - "CLOSE"
helpviewer_keywords:
  - "closing cursors"
  - "cursors [SQL Server], closing"
  - "CLOSE statement"
dev_langs:
  - "TSQL"
---

# CLOSE (Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Closes an open cursor by releasing the current result set and freeing any cursor locks held on the rows on which the cursor is positioned. `CLOSE` leaves the data structures available for reopening, but fetches and positioned updates are not allowed until the cursor is reopened. CLOSE must be issued on an open cursor; `CLOSE` is not allowed on cursors that have only been declared or are already closed.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
CLOSE { { [ GLOBAL ] cursor_name } | cursor_variable_name }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

GLOBAL  
Specifies that *cursor_name* refers to a global cursor.  
  
 *cursor_name*  
 Is the name of an open cursor. If both a global and a local cursor exist with *cursor_name* as their name, *cursor_name* refers to the global cursor when GLOBAL is specified; otherwise, *cursor_name* refers to the local cursor.  
  
 *cursor_variable_name*  
 Is the name of a cursor variable associated with an open cursor.  
  
## Examples

The following example shows the correct placement of the `CLOSE` statement in a cursor-based process.  
  
```sql  
DECLARE Employee_Cursor CURSOR FOR  
SELECT EmployeeID, Title FROM AdventureWorks2022.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## See Also

- [Cursors](../../relational-databases/cursors.md)
- [Cursors &#40;Transact-SQL&#41;](../../t-sql/language-elements/cursors-transact-sql.md)
- [DEALLOCATE &#40;Transact-SQL&#41;](../../t-sql/language-elements/deallocate-transact-sql.md)
- [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)
- [OPEN &#40;Transact-SQL&#41;](../../t-sql/language-elements/open-transact-sql.md)
