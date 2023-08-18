---
title: "LEAD (Transact-SQL)"
description: "LEAD (Transact-SQL)"
author: markingmyname
ms.author: maghan
ms.date: 07/26/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "LEAD_TSQL"
  - "LEAD"
helpviewer_keywords:
  - "LEAD function"
  - "analytic functions, LEAD"
dev_langs:
  - "TSQL"
monikerRange: ">= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || >= sql-server-linux-2017 || = azuresqldb-mi-current||=fabric"
---
# LEAD (Transact-SQL)
[!INCLUDE [sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw-fabricse-fabricdw.md)]

  Accesses data from a subsequent row in the same result set without the use of a self-join starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. LEAD provides access to a row at a given physical offset that follows the current row. Use this analytic function in a SELECT statement to compare values in the current row with values in a following row.  
  
 :::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## Syntax  
  
```syntaxsql  
LEAD ( scalar_expression [ , offset ] , [ default ] ) [ IGNORE NULLS | RESPECT NULLS ]
    OVER ( [ partition_by_clause ] order_by_clause )  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *scalar_expression*  

 The value to be returned based on the specified offset. It is an expression of any type that returns a single (scalar) value. *scalar_expression* cannot be an analytic function.  
  
 *offset*  
 The number of rows forward from the current row from which to obtain a value. If not specified, the default is 1. *offset* can be a column, subquery, or other expression that evaluates to a positive integer or can be implicitly converted to **bigint**. *offset* cannot be a negative value or an analytic function.  
  
 *default*  
 The value to return when *offset* is beyond the scope of the partition. If a default value is not specified, NULL is returned. *default* can be a column, subquery, or other expression, but it cannot be an analytic function. *default* must be type-compatible with *scalar_expression*.

#### [ IGNORE NULLS | RESPECT NULLS ]

**Applies to**: SQL Server (starting with [!INCLUDE[sssql22](../../includes/sssql22-md.md)]), Azure SQL Database, Azure SQL Managed Instance, [!INCLUDE[ssazurede-md](../../includes/ssazurede-md.md)]

IGNORE NULLS - Ignore NULL values in the dataset when computing the first value over a partition.

RESPECT NULLS - Respect NULL values in the dataset when computing first value over a partition. `RESPECT NULLS` is the default behavior if a NULLS option is not specified.

There was a [bug fix in SQL Server 2022 CU4](/troubleshoot/sql/releases/sqlserver-2022/cumulativeupdate4#2278800) related to IGNORE NULLS in `LAG` and `LEAD`.

For more information on this argument in [!INCLUDE[ssazurede-md](../../includes/ssazurede-md.md)], see [Imputing missing values](/azure/azure-sql-edge/imputing-missing-values/).

#### OVER ( [ *partition_by_clause* ] *order_by_clause* )

 *partition_by_clause* divides the result set produced by the FROM clause into partitions to which the function is applied. If not specified, the function treats all rows of the query result set as a single group. *order_by_clause* determines the order of the data before the function is applied. When *partition_by_clause* is specified, it determines the order of the data in each partition. The *order_by_clause* is required. For more information, see [OVER Clause (Transact-SQL)](../../t-sql/queries/select-over-clause-transact-sql.md).  
  
## Return Types  
 The data type of the specified *scalar_expression*. NULL is returned if *scalar_expression* is nullable or *default* is set to NULL.  
  
 LEAD is nondeterministic. For more information, see [Deterministic and Nondeterministic Functions](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md).  
  
## Examples  
  
### A. Compare values between years  
 The query uses the LEAD function to return the difference in sales quotas for a specific employee over subsequent years. Notice that because there is no lead value available for the last row, the default of zero (0) is returned.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT BusinessEntityID, YEAR(QuotaDate) AS SalesYear, SalesQuota AS CurrentQuota,   
    LEAD(SalesQuota, 1,0) OVER (ORDER BY YEAR(QuotaDate)) AS NextQuota  
FROM Sales.SalesPersonQuotaHistory  
WHERE BusinessEntityID = 275 AND YEAR(QuotaDate) IN ('2005','2006');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```output
BusinessEntityID SalesYear   CurrentQuota          NextQuota  
---------------- ----------- --------------------- ---------------------  
275              2005        367000.00             556000.00  
275              2005        556000.00             502000.00  
275              2006        502000.00             550000.00  
275              2006        550000.00             1429000.00  
275              2006        1429000.00            1324000.00  
275              2006        1324000.00            0.00  
```  
  
### B. Compare values within partitions  
 The following example uses the LEAD function to compare year-to-date sales between employees. The PARTITION BY clause is specified to partition the rows in the result set by sales territory. The LEAD function is applied to each partition separately and computation restarts for each partition. The ORDER BY clause specified in the OVER clause orders the rows in each partition before the function is applied. The ORDER BY clause in the SELECT statement orders the rows in the whole result set. Notice that because there is no lead value available for the last row of each partition, the default of zero (0) is returned.  
  
```sql  
USE AdventureWorks2022;  
GO  
SELECT TerritoryName, BusinessEntityID, SalesYTD,   
       LEAD (SalesYTD, 1, 0) OVER (PARTITION BY TerritoryName ORDER BY SalesYTD DESC) AS NextRepSales  
FROM Sales.vSalesPerson  
WHERE TerritoryName IN (N'Northwest', N'Canada')   
ORDER BY TerritoryName;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```output   
TerritoryName            BusinessEntityID SalesYTD              NextRepSales  
-----------------------  ---------------- --------------------- ---------------------  
Canada                   282              2604540.7172          1453719.4653  
Canada                   278              1453719.4653          0.00  
Northwest                284              1576562.1966          1573012.9383  
Northwest                283              1573012.9383          1352577.1325  
Northwest                280              1352577.1325          0.00  
  
```  
  
### C. Specifying arbitrary expressions  
 The following example demonstrates specifying various arbitrary expressions and ignoring NULL values in the LEAD function syntax.
  
```sql  
CREATE TABLE T (a INT, b INT, c INT);   
GO  
INSERT INTO T VALUES (1, 1, -3), (2, 2, 4), (3, 1, NULL), (4, 3, 1), (5, 2, NULL), (6, 1, 5);   
  
SELECT b, c,   
    LEAD(2*c, b*(SELECT MIN(b) FROM T), -c/2.0) IGNORE NULLS OVER (ORDER BY a) AS i  
FROM T;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```output  
b           c           i  
----------- ----------- -----------  
1           5           -2  
2           NULL        NULL  
3           1           0  
1           NULL        2  
2           4           2  
1           -3          8  
```  

### D. Use IGNORE NULLS to find non-NULL values

The following sample query demonstrates using the IGNORE NULLS argument.

The IGNORE NULLS argument is used with both [LAG](lag-transact-sql.md) and LEAD to demonstrate substitution of NULL values for preceding or next non-NULL values.

- If the preceding row contained NULL with `LAG`, then the current row uses the most recent non-NULL value.
- If the next row contains a NULL with `LEAD`, then the current row uses the next available non-NULL value.

```sql
DROP TABLE IF EXISTS #test_ignore_nulls;
CREATE TABLE #test_ignore_nulls (column_a int, column_b int);
GO

INSERT INTO #test_ignore_nulls VALUES
    (1, 8),
    (2, 9),
    (3, NULL),
    (4, 10),
    (5, NULL),
    (6, NULL),
    (7, 11);

SELECT column_a, column_b,
      [Previous value for column_b] = LAG(column_b) IGNORE NULLS OVER (ORDER BY column_a),
      [Next value for column_b] = LEAD(column_b) IGNORE NULLS OVER (ORDER BY column_a)
FROM #test_ignore_nulls
ORDER BY column_a;

--cleanup
DROP TABLE #test_ignore_nulls;
```

```output
column_a     column_b    Previous value for column_b    Next value for column_b
1            8           NULL                           9
2            9           8                              10
3            NULL        9                              10
4            10          9                              11
5            NULL        10                             11
6            NULL        10                             11
7            11          10                             NULL
```

### E. Use RESPECT NULLS to keep NULL values

The following sample query demonstrates using the RESPECT NULLS argument, which is the default behavior if not specified, as opposed to the IGNORE NULLS argument in the previous example.

- If the preceding row contained NULL with `LAG`, then the current row uses the most recent value.
- If the next row contains a NULL with `LEAD`, then the current row uses the next value.

```sql
DROP TABLE IF EXISTS #test_ignore_nulls;
CREATE TABLE #test_ignore_nulls (column_a int, column_b int);
GO

INSERT INTO #test_ignore_nulls VALUES
    (1, 8),
    (2, 9),
    (3, NULL),
    (4, 10),
    (5, NULL),
    (6, NULL),
    (7, 11);

SELECT column_a, column_b,
      [Previous value for column_b] = LAG(column_b) RESPECT NULLS OVER (ORDER BY column_a),
      [Next value for column_b] = LEAD(column_b) RESPECT NULLS OVER (ORDER BY column_a)
FROM #test_ignore_nulls
ORDER BY column_a;

--Identical output
SELECT column_a, column_b,
      [Previous value for column_b] = LAG(column_b)  OVER (ORDER BY column_a),
      [Next value for column_b] = LEAD(column_b)  OVER (ORDER BY column_a)
FROM #test_ignore_nulls
ORDER BY column_a;

--cleanup
DROP TABLE #test_ignore_nulls;
```

```output
column_a     column_b    Previous value for column_b    Next value for column_b
1            8           NULL                           9
2            9           8                              NULL
3            NULL        9                              10
4            10          NULL                           NULL
5            NULL        10                             NULL
6            NULL        NULL                           11
7            11          NULL                           NULL
```

## Examples: [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] and [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### A. Compare values between quarters  
 The following example demonstrates the LEAD function. The query obtains the difference in sales quota values for a specified employee over subsequent calendar quarters. Notice that because there is no lead value available after the last row, the default of zero (0) is used.  
  
```sql  
-- Uses AdventureWorks  
  
SELECT CalendarYear AS Year, CalendarQuarter AS Quarter, SalesAmountQuota AS SalesQuota,  
       LEAD(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS NextQuota,  
   SalesAmountQuota - LEAD(SalesAmountQuota,1,0) OVER (ORDER BY CalendarYear, CalendarQuarter) AS Diff  
FROM dbo.FactSalesQuota  
WHERE EmployeeKey = 272 AND CalendarYear IN (2001,2002)  
ORDER BY CalendarYear, CalendarQuarter;  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```output
Year Quarter  SalesQuota  NextQuota  Diff  
---- -------  ----------  ---------  -------------  
2001 3        28000.0000   7000.0000   21000.0000 
2001 4         7000.0000  91000.0000  -84000.0000  
2001 1        91000.0000 140000.0000  -49000.0000  
2002 2       140000.0000   7000.0000    7000.0000  
2002 3         7000.0000 154000.0000   84000.0000  
2002 4       154000.0000      0.0000  154000.0000
```  
  
## Next steps  

- [LAG (Transact-SQL)](../../t-sql/functions/lag-transact-sql.md)  
- [FIRST_VALUE (Transact-SQL)](first-value-transact-sql.md)
- [LAST_VALUE (Transact-SQL)](last-value-transact-sql.md)
- [SELECT - OVER Clause (Transact-SQL)](../queries/select-over-clause-transact-sql.md)