---
title: "PERCENT_RANK (Transact-SQL)"
description: "PERCENT_RANK (Transact-SQL)"
author: MikeRayMSFT
ms.author: mikeray
ms.date: "10/20/2015"
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "PERCENT_RANK_TSQL"
  - "PERCENT_RANK"
helpviewer_keywords:
  - "PERCENT_RANK function"
  - "analytic functions, PERCENT_RANK"
dev_langs:
  - "TSQL"
monikerRange: "= azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqldb-mi-current||=fabric"
---
# PERCENT_RANK (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-fabricse-fabricdw.md)]

  Calculates the relative rank of a row within a group of rows in [!INCLUDE[ssnoversion](../../includes/ssnoversion-md.md)]. Use PERCENT_RANK to evaluate the relative standing of a value within a query result set or partition. PERCENT_RANK is similar to the CUME_DIST function.  
  
## Syntax  
  
```syntaxsql  
PERCENT_RANK( )  
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments
 OVER **(** [ _partition\_by\_clause_ ] _order\_by\_clause_**)**  
 *partition_by_clause* divides the result set produced by the FROM clause into partitions to which the function is applied. If not specified, the function treats all rows of the query result set as a single group. _order\_by\_clause_ determines the logical order in which the operation is performed. The *order_by_clause* is required. The \<rows or range clause\> of the OVER syntax cannot be specified in a PERCENT_RANK function.  For more information, see [OVER Clause &#40;Transact-SQL&#41;](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## Return Types  
 **float(53)**  
  
## General Remarks  
 The range of values returned by PERCENT_RANK is greater than 0 and less than or equal to 1. The first row in any set has a PERCENT_RANK of 0. NULL values are included by default and are treated as the lowest possible values.  
  
 PERCENT_RANK is nondeterministic. For more information, see [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## Examples  
 The following example uses the CUME_DIST function to compute the salary percentile for each employee within a given department. The value returned by the CUME_DIST function represents the percent of employees that have a salary less than or equal to the current employee in the same department. The PERCENT_RANK function computes the rank of the employee's salary within a department as a percentage. The PARTITION BY clause is specified to partition the rows in the result set by department. The ORDER BY clause in the OVER clause orders the rows in each partition. The ORDER BY clause in the SELECT statement sorts the rows in the whole result set.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT Department, LastName, Rate,   
       CUME_DIST () OVER (PARTITION BY Department ORDER BY Rate) AS CumeDist,   
       PERCENT_RANK() OVER (PARTITION BY Department ORDER BY Rate ) AS PctRank  
FROM HumanResources.vEmployeeDepartmentHistory AS edh  
    INNER JOIN HumanResources.EmployeePayHistory AS e    
    ON e.BusinessEntityID = edh.BusinessEntityID  
WHERE Department IN (N'Information Services',N'Document Control')   
ORDER BY Department, Rate DESC;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
  
Department             LastName               Rate                  CumeDist               PctRank  
---------------------- ---------------------- --------------------- ---------------------- ----------------------  
Document Control       Arifin                 17.7885               1                      1  
Document Control       Norred                 16.8269               0.8                    0.5  
Document Control       Kharatishvili          16.8269               0.8                    0.5  
Document Control       Chai                   10.25                 0.4                    0  
Document Control       Berge                  10.25                 0.4                    0  
Information Services   Trenary                50.4808               1                      1  
Information Services   Conroy                 39.6635               0.9                    0.888888888888889  
Information Services   Ajenstat               38.4615               0.8                    0.666666666666667  
Information Services   Wilson                 38.4615               0.8                    0.666666666666667  
Information Services   Sharma                 32.4519               0.6                    0.444444444444444  
Information Services   Connelly               32.4519               0.6                    0.444444444444444  
Information Services   Berg                   27.4038               0.4                    0  
Information Services   Meyyappan              27.4038               0.4                    0  
Information Services   Bacon                  27.4038               0.4                    0  
Information Services   Bueno                  27.4038               0.4                    0  
(15 row(s) affected)  
```  
  
## See Also  
 [CUME_DIST &#40;Transact-SQL&#41;](../../t-sql/functions/cume-dist-transact-sql.md)  
  
  
