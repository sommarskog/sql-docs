---
title: ISNULL (Transact-SQL)
description: "ISNULL (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: "03/06/2017"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ISNULL"
  - "ISNULL_TSQL"
  - "IFNULL_TSQL"
helpviewer_keywords:
  - "replacing null values"
  - "null values [SQL Server], ISNULL"
  - "null values [SQL Server], replacement values"
  - "ISNULL function"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqldb-mi-current||=fabric"
---

# ISNULL (Transact-SQL) 

[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Replaces NULL with the specified replacement value.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
ISNULL ( check_expression , replacement_value )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 *check_expression*  
 Is the [expression](../../t-sql/language-elements/expressions-transact-sql.md) to be checked for NULL. *check_expression* can be of any type.  
  
 *replacement_value*  
 Is the expression to be returned if *check_expression* is NULL. *replacement_value* must be of a type that is implicitly convertible to the type of *check_expression*.  
  
## Return Types  
 Returns the same type as *check_expression*. If a literal NULL is provided as *check_expression*, returns the datatype of the *replacement_value*. If a literal NULL is provided as *check_expression* and no *replacement_value* is provided, returns an **int**.  
  
## Remarks  
 The value of *check_expression* is returned if it is not NULL; otherwise, *replacement_value* is returned after it is implicitly converted to the type of *check_expression*, if the types are different. *replacement_value* can be truncated if *replacement_value* is longer than *check_expression*.  
  
> [!NOTE]  
>  Use [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md) to return the first non-null value.  
  
## Examples  
  
### A. Using ISNULL with AVG  
 The following example finds the average of the weight of all products. It substitutes the value `50` for all NULL entries in the `Weight` column of the `Product` table.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT AVG(ISNULL(Weight, 50))  
FROM Production.Product;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
 -------------------------- 
59.79  
  
 (1 row(s) affected)
 ```  
  
### B. Using ISNULL  
 The following example selects the description, discount percentage, minimum quantity, and maximum quantity for all special offers in [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)]. If the maximum quantity for a particular special offer is NULL, the `MaxQty` shown in the result set is `0.00`.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT Description, DiscountPct, MinQty, ISNULL(MaxQty, 0.00) AS 'Max Quantity'  
FROM Sales.SpecialOffer;  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|  Description       |  DiscountPct    |   MinQty    |   Max Quantity       |
|  ---------------   |  -------------  |   --------  |   ---------------    |
|  No Discount       |  0.00           |   0         |   0                  |
|  Volume Discount   |  0.02           |   11        |   14                 |
|  Volume Discount   |  0.05           |   15        |   4                  |
|  Volume Discount   |  0.10           |   25        |   0                  |
|  Volume Discount   |  0.15           |   41        |   0                  |
|  Volume Discount   |  0.20           |   61        |   0                  |
|  Mountain-100 Cl   |  0.35           |   0         |   0                  |
|  Sport Helmet Di   |  0.10           |   0         |   0                  |
|  Road-650 Overst   |  0.30           |   0         |   0                  |
|  Mountain Tire S   |  0.50           |   0         |   0                  |
|  Sport Helmet Di   |  0.15           |   0         |   0                  |
|  LL Road Frame S   |  0.35           |   0         |   0                  |
|  Touring-3000 Pr   |  0.15           |   0         |   0                  |
|  Touring-1000 Pr   |  0.20           |   0         |   0                  |
|  Half-Price Peda   |  0.50           |   0         |   0                  |
|  Mountain-500 Si   |  0.40           |   0         |   0                  |

 `(16 row(s) affected)`  
  
### C. Testing for NULL in a WHERE clause  
 Do not use ISNULL to find NULL values. Use IS NULL instead. The following example finds all products that have `NULL` in the weight column. Note the space between `IS` and `NULL`.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT Name, Weight  
FROM Production.Product  
WHERE Weight IS NULL;  
GO  
```  
  
## Examples: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### D. Using ISNULL with AVG  
 The following example finds the average of the weight of all products in a sample table. It substitutes the value `50` for all NULL entries in the `Weight` column of the `Product` table.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT AVG(ISNULL(Weight, 50))  
FROM dbo.DimProduct;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
--------------------------   
52.88   
```  
  
### E. Using ISNULL  
 The following example uses ISNULL to test for NULL values in the column `MinPaymentAmount` and display the value `0.00` for those rows.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT ResellerName,   
       ISNULL(MinPaymentAmount,0) AS MinimumPayment  
FROM dbo.DimReseller  
ORDER BY ResellerName;  
  
```  
  
 Here is a partial result set.  
  
|  ResellerName                |  MinimumPayment    |
|  -------------------------   |  --------------    |
|  A Bicycle Association       |     0.0000         |
|  A Bike Store                |     0.0000         |
|  A Cycle Shop                |     0.0000         |
|  A Great Bicycle Company     |     0.0000         |
|  A Typical Bike Shop         |   200.0000         |
|  Acceptable Sales & Service  |     0.0000         |
  
### F. Using IS NULL to test for NULL in a WHERE clause  
 The following example finds all products that have `NULL` in the `Weight` column. Note the space between `IS` and `NULL`.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT EnglishProductName, Weight  
FROM dbo.DimProduct  
WHERE Weight IS NULL;  
```  
  
## See Also  
 [Expressions &#40;Transact-SQL&#41;](../../t-sql/language-elements/expressions-transact-sql.md)   
 [IS NULL &#40;Transact-SQL&#41;](../../t-sql/queries/is-null-transact-sql.md)   
 [System Functions &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-category-transact-sql.md)   
 [WHERE &#40;Transact-SQL&#41;](../../t-sql/queries/where-transact-sql.md)   
 [COALESCE &#40;Transact-SQL&#41;](../../t-sql/language-elements/coalesce-transact-sql.md)  
  
  

