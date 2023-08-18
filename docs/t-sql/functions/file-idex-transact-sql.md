---
title: "FILE_IDEX (Transact-SQL)"
description: "FILE_IDEX (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/03/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "FILE_IDEX"
  - "FILE_IDEX_TSQL"
helpviewer_keywords:
  - "FILE_IDEX function"
  - "IDs [SQL Server], files"
  - "file IDs [SQL Server]"
  - "names [SQL Server], files"
  - "identification numbers [SQL Server], files"
  - "file names [SQL Server], FILE_IDEX"
dev_langs:
  - "TSQL"
---
# FILE_IDEX (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdbmi.md)]

This function returns the file identification (ID) number for the specified logical name of a data, log, or full-text file of the current database. 
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql  
FILE_IDEX ( file_name )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *file_name*  
An expression of type **sysname** that returns the file ID value 'FILE_IDEX' for the name of the file. 
  
## Return Types  
**int**  
  
**NULL** on error  
  
## Remarks  
*file_name* corresponds to the logical file name displayed in the **name** column from the [sys.master_files](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md) or [sys.database_files](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md) catalog views.  
  
Use `FILE_IDEX` in a SELECT list, a WHERE clause, or anywhere that supports use of an expression. For more information, see [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md).  
  
## Examples  
  
### A. Retrieving the file id of a specified file  
This example returns the file ID for the `AdventureWorks_Data` file.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT FILE_IDEX('AdventureWorks2022_Data') AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
1  
(1 row(s) affected)  
```  
  
### B. Retrieving the file id when the file name is not known  
This example returns the file ID of the `AdventureWorks` log file. The Transact-SQL (T-SQL) code snippet selects the logical file name from the `sys.database_files` catalog view, where the file type equals `1` (log).  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT FILE_IDEX((SELECT TOP (1) name FROM sys.database_files WHERE type = 1)) AS 'File ID';  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
File ID   
-------   
2  
```  
  
### C. Retrieving the file id of a full-text catalog file  
This example returns the file ID of a full-text file. The T-SQL code snippet selects the logical file name from the `sys.database_files` catalog view, where the file type equals `4` (full-text). This code returns 'NULL' if a full-text catalog does not exist.
  
```sql  
SELECT FILE_IDEX((SELECT name FROM sys.master_files WHERE type = 4))  
AS 'File_ID';  
```  
  
## See Also  
 [Metadata Functions &#40;Transact-SQL&#41;](../../t-sql/functions/metadata-functions-transact-sql.md)   
 [sys.database_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.master_files &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-master-files-transact-sql.md)  
  
  
