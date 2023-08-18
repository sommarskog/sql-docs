---
title: "DATABASE_PRINCIPAL_ID (Transact-SQL)"
description: "DATABASE_PRINCIPAL_ID (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "05/14/2019"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "DATABASE_PRINCIPAL_ID_TSQL"
  - "DATABASE_PRINCIPAL_ID"
helpviewer_keywords:
  - "identification numbers [SQL Server], principals"
  - "principal ID numbers [SQL Server]"
  - "DATABASE_PRINCIPAL_ID function"
  - "IDs [SQL Server], principals"
dev_langs:
  - "TSQL"
monikerRange: "= azuresqldb-current || = azuresqldb-mi-current || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqledge-current || = azure-sqldw-latest"
---
# DATABASE_PRINCIPAL_ID (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

This function returns the ID number of a principal in the current database. See [Principals &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md) for more information about principals.
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## Syntax  
  
```syntaxsql
DATABASE_PRINCIPAL_ID ( 'principal_name' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
*principal_name*  
An expression of type **sysname**, that represents the principal. When *principal_name* is omitted, `DATABASE_PRINCIPAL_ID` returns the ID of the current user. `DATABASE_PRINCIPAL_ID` requires the parentheses.
  
## Return types
**int**  
NULL if the database principal does not exist.
  
## Remarks  
Use `DATABASE_PRINCIPAL_ID` in a select list, a WHERE clause, or any place that allows an expression. See [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md) for more information.
  
## Examples  
  
### A. Retrieving the ID of the current user  
This example returns the database principal ID of the current user.
  
```sql
SELECT DATABASE_PRINCIPAL_ID();  
GO  
```  
  
### B. Retrieving the ID of a specified database principal  
This example returns the database principal ID for the database role `db_owner`.
  
```sql
SELECT DATABASE_PRINCIPAL_ID('db_owner');  
GO  
```  
  
## See also
[Principals &#40;Database Engine&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)  
[Permissions Hierarchy &#40;Database Engine&#41;](../../relational-databases/security/permissions-hierarchy-database-engine.md)  
[sys.database_principals &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)
  
  
