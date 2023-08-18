---
title: "SET NUMERIC_ROUNDABORT (Transact-SQL)"
description: SET NUMERIC_ROUNDABORT (Transact-SQL)
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.date: "12/04/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "NUMERIC_ROUNDABORT"
  - "SET_NUMERIC_ROUNDABORT_TSQL"
  - "SET NUMERIC_ROUNDABORT"
  - "NUMERIC_ROUNDABORT_TSQL"
helpviewer_keywords:
  - "rounding expressions"
  - "precision [SQL Server], rounded expressions"
  - "expressions [SQL Server], rounding"
  - "NUMERIC_ROUNDABORT"
  - "SET NUMERIC_ROUNDABORT statement"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# SET NUMERIC_ROUNDABORT (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Specifies the level of error reporting generated when rounding in an expression causes a loss of precision.  
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

## Syntax

```syntaxsql

SET NUMERIC_ROUNDABORT { ON | OFF }
```
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Remarks
When SET NUMERIC_ROUNDABORT is ON, an error is generated after a loss of precision occurs in an expression. If set to OFF, losses of precision don't generate error messages. The result is rounded to the precision of the column or variable storing the result.  
  
Loss of precision occurs when you attempt to store a value with fixed precision in a column or variable with less precision.  
  
If SET NUMERIC_ROUNDABORT is ON, SET ARITHABORT determines the severity of the generated error. This table shows the effects of these two settings when a loss of precision occurs.  
  
|Setting|SET NUMERIC_ROUNDABORT ON|SET NUMERIC_ROUNDABORT OFF|
|-------------|--------------------------------|---------------------------------|
|SET ARITHABORT ON|Error is generated; no set of results returned.|No errors or warnings; result is rounded.|  
|SET ARITHABORT OFF|Warning is returned; expression returns NULL.|No errors or warnings; result is rounded.|  

The setting of SET NUMERIC_ROUNDABORT is set at execute or run time and not at parse time.

SET NUMERIC_ROUNDABORT must be OFF when you're creating or changing indexes on computed columns or indexed views. If SET NUMERIC_ROUNDABORT is ON, the following statements on tables with indexes on computed columns or indexed views fail:

- CREATE 
- UPDATE 
- INSERT 
- DELETE 

For more information about required SET option settings with indexed views and indexes on computed columns, see [Considerations When You Use the SET Statements](../../t-sql/statements/set-statements-transact-sql.md#considerations-when-you-use-the-set-statements).
  
To view the current setting for this setting, run the following query:
  
```sql
DECLARE @NUMERIC_ROUNDABORT VARCHAR(3) = 'OFF';  
IF ( (8192 & @@OPTIONS) = 8192 ) SET @NUMERIC_ROUNDABORT = 'ON';  
SELECT @NUMERIC_ROUNDABORT AS NUMERIC_ROUNDABORT;  
  
```  
  
## Permissions  
Requires membership in the **public** role.  
  
## Examples  
The following example shows two values that are precise to four decimal places. They get added and stored in a variable that is precise to two decimal places. The expressions demonstrate the effects of the different `SET NUMERIC_ROUNDABORT` and `SET ARITHABORT` settings.  
  
```sql
-- SET NOCOUNT to ON,   
-- SET NUMERIC_ROUNDABORT to ON, and SET ARITHABORT to ON.  
SET NOCOUNT ON;  
PRINT 'SET NUMERIC_ROUNDABORT ON';  
PRINT 'SET ARITHABORT ON';  
SET NUMERIC_ROUNDABORT ON;  
SET ARITHABORT ON;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to ON and SET ARITHABORT to OFF.  
PRINT 'SET NUMERIC_ROUNDABORT ON';  
PRINT 'SET ARITHABORT OFF';  
SET NUMERIC_ROUNDABORT ON;  
SET ARITHABORT OFF;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to OFF and SET ARITHABORT to ON.  
PRINT 'SET NUMERIC_ROUNDABORT OFF';  
PRINT 'SET ARITHABORT ON';  
SET NUMERIC_ROUNDABORT OFF;  
SET ARITHABORT ON;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234 ;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
  
-- SET NUMERIC_ROUNDABORT to OFF and SET ARITHABORT to OFF.  
PRINT 'SET NUMERIC_ROUNDABORT OFF';  
PRINT 'SET ARITHABORT OFF';  
SET NUMERIC_ROUNDABORT OFF;  
SET ARITHABORT OFF;  
GO  
DECLARE @result DECIMAL(5, 2),  
   @value_1 DECIMAL(5, 4),   
   @value_2 DECIMAL(5, 4);  
SET @value_1 = 1.1234;  
SET @value_2 = 1.1234;  
SELECT @result = @value_1 + @value_2;  
SELECT @result;  
GO  
```  
  
## See Also  
[Data Types &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
[SET Statements &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)   
[SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)  
  
  
