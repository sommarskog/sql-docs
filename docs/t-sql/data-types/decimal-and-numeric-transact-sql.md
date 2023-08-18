---
title: "decimal and numeric (Transact-SQL)"
description: "Transact-SQL reference for the decimal and numeric data types. Decimal and numeric are synonyms for numeric data types that have a fixed precision and scale."
author: MikeRayMSFT
ms.author: mikeray
ms.date: "09/10/2019"
ms.service: sql
ms.subservice: t-sql
ms.topic: "reference"
f1_keywords:
  - "decimal"
  - "decimal_TSQL"
  - "numeric"
  - "numeric_TSQL"
helpviewer_keywords:
  - "decimal data type"
  - "decimal data type, about decimal data type"
  - "numeric data type"
  - "numeric data type, about numeric data type"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current||=fabric"
---
# decimal and numeric (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Numeric data types that have fixed precision and scale. Decimal and numeric are synonyms and can be used interchangeably.
  
## Arguments
**decimal**[ **(**_p_[ **,**_s_] **)**] and **numeric**[ **(**_p_[ **,**_s_] **)**]  
Fixed precision and scale numbers. When maximum precision is used, valid values are from - 10^38 +1 through 10^38 - 1. The ISO synonyms for **decimal** are **dec** and **dec(**_p_, _s_**)**. **numeric** is functionally identical to **decimal**.
  
p (precision)  
The maximum total number of decimal digits to be stored. This number includes both the left and the right sides of the decimal point. The precision must be a value from 1 through the maximum precision of 38. The default precision is 18.
  
> [!NOTE]  
>  Informatica only supports 16 significant digits, regardless of the precision and scale specified.  

*s* (scale)  
The number of decimal digits that are stored to the right of the decimal point. This number is subtracted from *p* to determine the maximum number of digits to the left of the decimal point. Scale must be a value from 0 through *p*, and can only be specified if precision is specified. The default scale is 0 and so 0 <= *s* \<= *p*. Maximum storage sizes vary, based on the precision.
  
|Precision|Storage bytes|  
|---|---|
|1 - 9|5|  
|10-19|9|  
|20-28|13|  
|29-38|17|  
  
> [!NOTE]  
>  Informatica (connected through the SQL Server PDW Informatica Connector) only supports 16 significant digits, regardless of the precision and scale specified.  
  
## Converting decimal and numeric data
For **decimal** and **numeric** data types, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] considers each combination of precision and scale as a different data type. For example, **decimal(5,5)** and **decimal(5,0)** are considered different data types.
  
In [!INCLUDE[tsql](../../includes/tsql-md.md)] statements, a constant with a decimal point is automatically converted into a **numeric** data value, using the minimum precision and scale necessary. For example, the constant 12.345 is converted into a **numeric** value with a precision of 5 and a scale of 3.
  
Converting from **decimal** or **numeric** to **float** or **real** can cause some loss of precision. Converting from **int**, **smallint**, **tinyint**, **float**, **real**, **money**, or **smallmoney** to either **decimal** or **numeric** can cause overflow.
  
By default, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] uses rounding when converting a number to a **decimal** or **numeric** value with a lower precision and scale. Conversely, if the SET ARITHABORT option is ON, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] raises an error when overflow occurs. Loss of only precision and scale isn't sufficient to raise an error.
  
Prior to [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)], conversion of **float** values to **decimal** or **numeric** is restricted to values of precision 17 digits only. Any **float** value less than 5E-18 (when set using either the scientific notation of 5E-18 or the decimal notation of 0.000000000000000005) rounds down to 0. This is no longer a restriction as of [!INCLUDE[ssSQL16](../../includes/sssql16-md.md)].
  
## Examples  
The following example creates a table using the **decimal** and **numeric** data types.  Values are inserted into each column. The results are returned by using a SELECT statement.
  
```sql
CREATE TABLE dbo.MyTable  
(  
  MyDecimalColumn DECIMAL(5,2)  
,MyNumericColumn NUMERIC(10,5)
  
);  
  
GO  
INSERT INTO dbo.MyTable VALUES (123, 12345.12);  
GO  
SELECT MyDecimalColumn, MyNumericColumn  
FROM dbo.MyTable;  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```sql
MyDecimalColumn                         MyNumericColumn  
--------------------------------------- ---------------------------------------  
123.00                                  12345.12000  
  
(1 row(s) affected)  
  
```  
  
## See also
[ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)  
[CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)  
[sys.types &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)
  
