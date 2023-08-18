---
title: "IDENT_INCR (Transact-SQL)"
description: "IDENT_INCR (Transact-SQL)"
author: VanMSFT
ms.author: vanto
ms.date: "03/14/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "IDENT_INCR"
  - "IDENT_INCR_TSQL"
helpviewer_keywords:
  - "incremental values [SQL Server]"
  - "IDENT_INCR function"
  - "identity columns [SQL Server], IDENT_INCR function"
dev_langs:
  - "TSQL"
---
# IDENT_INCR (Transact-SQL)
[!INCLUDE [SQL Server Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Returns the increment value specified when creating a table or view's identity column.  
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql 
IDENT_INCR ( 'table_or_view' )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
**'** *table_or_view* **'**  
Is an [expression](../../t-sql/language-elements/expressions-transact-sql.md) specifying the table or view to check for a valid identity increment value. *table_or_view* can be a character string constant enclosed in quotation marks. It can also be a variable, a function, or a column name. *table_or_view* is **char**, **nchar**, **varchar**, or **nvarchar**.  
  
## Return Types  
**numeric**([@@MAXPRECISION](../../t-sql/functions/max-precision-transact-sql.md),0))  
  
## Exceptions  
Returns NULL on error or if a caller doesn't have object view permission.  
  
In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a user can only view the metadata of securables they own or have permissions for. Without user object permission, a metadata-emitting, built-in function, such as IDENT_INCR, may return NULL. For more information, see [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## Examples  
  
### A. Returning the increment value for a specified table  
 The following example returns the increment value for the `Person.Address` table in the [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT IDENT_INCR('Person.Address') AS Identity_Increment;  
GO  
```  
  
### B. Returning the increment value from multiple tables  
 The following example returns the tables in the [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] database that includes an identity column with an increment value.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT TABLE_SCHEMA, TABLE_NAME,   
   IDENT_INCR(TABLE_SCHEMA + '.' + TABLE_NAME) AS IDENT_INCR  
FROM INFORMATION_SCHEMA.TABLES  
WHERE IDENT_INCR(TABLE_SCHEMA + '.' + TABLE_NAME) IS NOT NULL;  
```  
  
 Here is a partial result set.  
  
 ```
 TABLE_SCHEMA        TABLE_NAME                IDENT_INCR  
------------        ------------------------  ----------  
Person              Address                            1  
Production          ProductReview                      1  
Production          TransactionHistory                 1  
Person              AddressType                        1  
Production          ProductSubcategory                 1  
Person              vAdditionalContactInfo             1  
dbo                 AWBuildVersion                     1  
Production          BillOfMaterials                    1
```  
  
## See Also  
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [System Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [IDENT_CURRENT &#40;Transact-SQL&#41;](../../t-sql/functions/ident-current-transact-sql.md)   
 [IDENT_SEED &#40;Transact-SQL&#41;](../../t-sql/functions/ident-seed-transact-sql.md)   
 [DBCC CHECKIDENT &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)   
 [sys.identity_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-identity-columns-transact-sql.md)  
  
  
