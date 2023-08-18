---
title: PERCENTILE_DISC (Transact-SQL)
description: "PERCENTILE_DISC (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "10/20/2015"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "PERCENTILE_DISC"
  - "PERCENTILE_DISC_TSQL"
helpviewer_keywords:
  - "PERCENTILE_DISC function"
  - "analytic functions,PERCENTILE_DISC"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqldb-mi-current||=fabric"
---

# PERCENTILE_DISC (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

Computes a specific percentile for sorted values in an entire rowset or within a rowset's distinct partitions in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For a given percentile value *P*, PERCENTILE_DISC sorts the expression values in the ORDER BY clause. It then returns the value with the smallest CUME_DIST value given (with respect to the same sort specification) that is greater than or equal to *P*. For example, PERCENTILE_DISC (0.5) will compute the 50th percentile (that is, the median) of an expression. PERCENTILE_DISC calculates the percentile based on a discrete distribution of the column values. The result is equal to a specific column value.  
  
:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql
PERCENTILE_DISC ( numeric_literal ) WITHIN GROUP ( ORDER BY order_by_expression [ ASC | DESC ] )  
    OVER ( [ <partition_by_clause> ] )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

*literal*  
 The percentile to compute. The value must range between 0.0 and 1.0.  
  
 WITHIN GROUP **(** ORDER BY *order_by_expression* [ **ASC** | DESC)**  
 Specifies a list of values to sort and compute the percentile over. Only one *order_by_expression* is allowed. The default sort order is ascending. The list of values can be of any of the data types that are valid for the sort operation.  
  
 OVER **(** \<partition_by_clause>)**  
 Divides the FROM clause's result set into partitions. The percentile function is applied to these partitions. For more information, see [OVER Clause &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md). The \<ORDER BY clause> and \<rows or range clause>can't be specified in a PERCENTILE_DISC function.  
  
## Return Types

The return type is determined by the *order_by_expression* type.  
  
## Compatibility Support  

Under compatibility level 110 and higher, WITHIN GROUP is a reserved keyword. For more information, see [ALTER DATABASE Compatibility Level &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  
  
## General Remarks  

Any nulls in the data set are ignored.  
  
PERCENTILE_DISC is nondeterministic. For more information, see [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## Examples  
  
### Basic syntax example  

The following example uses PERCENTILE_CONT and PERCENTILE_DISC to find  each department's median employee salary. They may not return the same value:

* PERCENTILE_CONT returns the appropriate value, even if it doesn't exist in the data set.
* PERCENTILE_DISC returns an actual set value.  
  
```sql
USE AdventureWorks2022;  
  
SELECT DISTINCT Name AS DepartmentName  
      ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianCont  
      ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY ph.Rate)   
                            OVER (PARTITION BY Name) AS MedianDisc  
FROM HumanResources.Department AS d  
INNER JOIN HumanResources.EmployeeDepartmentHistory AS dh   
    ON dh.DepartmentID = d.DepartmentID  
INNER JOIN HumanResources.EmployeePayHistory AS ph  
    ON ph.BusinessEntityID = dh.BusinessEntityID  
WHERE dh.EndDate IS NULL;  
```  
  
Here is a partial result set.  

```output
DepartmentName        MedianCont    MedianDisc
Document Control       16.8269      16.8269
Engineering            34.375       32.6923
Executive              54.32695     48.5577
Human Resources        17.427850    16.5865
```

## Examples: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### Basic syntax example

The following example uses PERCENTILE_CONT and PERCENTILE_DISC to find each department's median employee salary. They may not return the same value:

* PERCENTILE_CONT returns the appropriate value, even if it doesn't exist in the data set.
* PERCENTILE_DISC returns an actual set value.  
  
```sql
-- Uses AdventureWorks  
  
SELECT DISTINCT DepartmentName  
       ,PERCENTILE_CONT(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianCont  
       ,PERCENTILE_DISC(0.5) WITHIN GROUP (ORDER BY BaseRate)  
        OVER (PARTITION BY DepartmentName) AS MedianDisc  
FROM dbo.DimEmployee;  
```  
  
Here is a partial result set.  

```output
DepartmentName        MedianCont    MedianDisc  
--------------------   ----------   ----------  
Document Control       16.826900    16.8269  
Engineering            34.375000    32.6923  
Human Resources        17.427850    16.5865  
Shipping and Receiving  9.250000     9.0000
```

## See Also  

[PERCENTILE_CONT &#40;Transact-SQL&#41;](../../t-sql/functions/percentile-cont-transact-sql.md)
