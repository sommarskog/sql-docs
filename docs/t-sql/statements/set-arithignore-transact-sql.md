---
title: "SET ARITHIGNORE (Transact-SQL)"
description: SET ARITHIGNORE (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "12/04/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "SET ARITHIGNORE"
  - "SET_ARITHIGNORE_TSQL"
  - "ARITHIGNORE"
  - "ARITHIGNORE_TSQL"
helpviewer_keywords:
  - "SET ARITHIGNORE statement"
  - "overflow errors [SQL Server]"
  - "ARITHIGNORE option"
  - "divide-by-zero errors"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# SET ARITHIGNORE (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Controls whether error messages are returned from overflow or divide-by-zero errors during a query.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
-- Syntax for SQL Server and Azure SQL Database and Microsoft Fabric

SET ARITHIGNORE { ON | OFF }
```

```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse  

SET ARITHIGNORE OFF
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

> [!NOTE]
> [!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## Remarks
 The SET ARITHIGNORE setting only controls whether an error message is returned. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] returns a NULL in a calculation involving an overflow or divide-by-zero error, regardless of this setting. The SET ARITHABORT setting can be used to determine whether the query is terminated. This setting does not affect errors occurring during INSERT, UPDATE, and DELETE statements.  
  
 If either SET ARITHABORT or SET ARITHIGNORE is OFF and SET ANSI_WARNINGS is ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] still returns an error message when encountering divide-by-zero or overflow errors.  
  
 The setting of SET ARITHIGNORE is set at execute or run time and not at parse time.  
  
 To view the current setting for this setting, run the following query.  
  
```sql  
DECLARE @ARITHIGNORE VARCHAR(3) = 'OFF';  
IF ( (128 & @@OPTIONS) = 128 ) SET @ARITHIGNORE = 'ON';  
SELECT @ARITHIGNORE AS ARITHIGNORE;  
```  
  
## Permissions  
 Requires membership in the public role.  
  
## Examples  
 The following example demonstrates using both `SET ARITHIGNORE` settings with both types of query errors.  
  
```sql  
SET ARITHABORT OFF;  
SET ANSI_WARNINGS OFF  
GO  
  
PRINT 'Setting ARITHIGNORE ON';  
GO  
-- SET ARITHIGNORE ON and testing.  
SET ARITHIGNORE ON;  
GO  
SELECT 1 / 0 AS DivideByZero;  
GO  
SELECT CAST(256 AS TINYINT) AS Overflow;  
GO  
  
PRINT 'Setting ARITHIGNORE OFF';  
GO  
-- SET ARITHIGNORE OFF and testing.  
SET ARITHIGNORE OFF;  
GO  
SELECT 1 / 0 AS DivideByZero;  
GO  
SELECT CAST(256 AS TINYINT) AS Overflow;  
GO  
```  
  
## Examples: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 The following example demonstrates the divide by zero and the overflow errors. This example does not return an error message for these errors because ARITHIGNORE is OFF.  
  
```sql  
-- SET ARITHIGNORE OFF and testing.  
SET ARITHIGNORE OFF;  
SELECT 1 / 0 AS DivideByZero;  
SELECT CAST(256 AS TINYINT) AS Overflow;  
```  
  
## See Also  
 [SET Statements &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)  
  
  

