---
title: Query data in a system-versioned temporal table
description: Use FOR SYSTEM_TIME clause to query data in temporal tables.
author: rwestMSFT
ms.author: randolphwest
ms.date: 03/27/2023
ms.service: sql
ms.subservice: table-view-index
ms.topic: conceptual
monikerRange: "=azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---
# Query data in a system-versioned temporal table

[!INCLUDE [sqlserver2016-asdb-asdbmi](../../includes/applies-to-version/sqlserver2016-asdb-asdbmi.md)]

When you want to get latest (current) state of data in a temporal table, you can query the same way as you query a non-temporal table. If the `PERIOD` columns aren't hidden, their values appear in a `SELECT *` query. If you specified `PERIOD` columns as `HIDDEN`, their values don't appear in a `SELECT *` query. When the `PERIOD` columns are hidden, you must reference the `PERIOD` columns specifically in the `SELECT` clause to return the values for these columns.

To perform any type of time-based analysis, use the new `FOR SYSTEM_TIME` clause with four temporal-specific subclauses to query data across the current and history tables. For more information on these clauses, see [Temporal Tables](temporal-tables.md) and [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)

- `AS OF <date_time>`
- `FROM <start_date_time> TO <end_date_time>`
- `BETWEEN <start_date_time> AND <end_date_time>`
- `CONTAINED IN (<start_date_time>, <end_date_time>)`
- `ALL`

`FOR SYSTEM_TIME` can be specified independently for each table in a query. It can be used inside common table expressions, table-valued functions, and stored procedures. When using a table alias with a temporal table, the `FOR SYSTEM_TIME` clause must be included between the temporal table name and the alias (see [Query for a specific time using the `AS OF` subclause](#query-for-a-specific-time-using-the-as-of-subclause) second example).

## Query for a specific time using the `AS OF` subclause

Use the `AS OF` subclause when you need to reconstruct state of data as it was at any specific time in the past. You can reconstruct the data with the precision of datetime2 type that was specified in `PERIOD` column definitions.

The `AS OF` subclause can be used with constant literals or with variables, so that you can dynamically specify the time condition. The values provided are interpreted as UTC time.

This first example returns the state of the dbo.Department table `AS OF` a specific date in the past.

```sql
/*State of entire table AS OF specific date in the past*/
SELECT [DeptID],
    [DeptName],
    [ValidFrom],
    [ValidTo]
FROM [dbo].[Department]
FOR SYSTEM_TIME AS OF '2021-09-01 T10:00:00.7230011';
```

This second example compares the values between two points in time for a subset of rows.

```sql
DECLARE @ADayAgo DATETIME2;
SET @ADayAgo = DATEADD(day, -1, sysutcdatetime());

/*Comparison between two points in time for subset of rows*/
SELECT D_1_Ago.[DeptID],
    D.[DeptID],
    D_1_Ago.[DeptName],
    D.[DeptName],
    D_1_Ago.[ValidFrom],
    D.[ValidFrom],
    D_1_Ago.[ValidTo],
    D.[ValidTo]
FROM [dbo].[Department]
FOR SYSTEM_TIME AS OF @ADayAgo AS D_1_Ago
INNER JOIN [Department] AS D
    ON D_1_Ago.[DeptID] = [D].[DeptID]
        AND D_1_Ago.[DeptID] BETWEEN 1 AND 5;
```

### Use views with `AS OF` subclause in temporal queries

Using views is useful in scenarios when complex point-in time analysis is required. A common example is generating a business report today with the values for previous month.

Usually, customers have a normalized database model, which involves many tables with foreign key relationships. Finding out how data from that normalized model looked at a point in the past can be challenging, since all tables change independently on their own cadence.

In this case, the best option is to create a view and apply the `AS OF` subclause to the entire view. Using this approach allows you to decouple modeling of the data access layer from point-in time analysis, as SQL Server applies `AS OF` clause transparently to all temporal tables that participate in view definition. Furthermore, you can combine temporal with non-temporal tables in the same view and `AS OF` is applied only to temporal ones. If the view doesn't reference at least one temporal table, applying temporal querying clauses to it fails with an error.

The following sample code creates a view that joins three temporal tables: `Department`, `CompanyLocation`, and `LocationDepartments`:

```sql
CREATE VIEW [dbo].[vw_GetOrgChart]
AS
SELECT [CompanyLocation].LocID,
    [CompanyLocation].LocName,
    [CompanyLocation].City,
    [Department].DeptID,
    [Department].DeptName
FROM [dbo].[CompanyLocation]
LEFT JOIN [dbo].[LocationDepartments]
    ON [CompanyLocation].LocID = LocationDepartments.LocID
LEFT JOIN [dbo].[Department]
    ON LocationDepartments.DeptID = [Department].DeptID;
GO
```

You can now query the view using the `AS OF` subclause and a **datetime2** literal:

```sql
/* Querying view AS OF */
SELECT * FROM [vw_GetOrgChart]
FOR SYSTEM_TIME AS OF'2021-09-01 T10:00:00.7230011';
```

Alternatively, you can query the view using the `AS OF` subclause with a local time zone and `AT TIME ZONE`:

```sql
/* Querying view AS OF with local time*/
DECLARE @LocalTime DATETIMEOFFSET = '2021-09-01 10:00:00.7230011 -07:00';

SELECT * FROM [vw_GetOrgChart]
FOR SYSTEM_TIME AS OF @LocalTime AT TIME ZONE 'UTC';
```

## Query for changes to specific rows over time

The temporal subclauses `FROM ... TO`, `BETWEEN ... AND` and `CONTAINED IN` are useful when you need to get all historical changes for a specific row in the current table (also known as a data audit).

The first two subclauses return row versions that overlap with a specified period (that is, those that started before given period and ended after it), while `CONTAINED IN` returns only those that existed within specified period boundaries.

If you search for non-current row versions only, you should query the history table directly, for best query performance. Use `ALL` when you need to query current and historical data without any restrictions.

```sql
/* Query using BETWEEN...AND sub-clause*/
SELECT [DeptID],
    [DeptName],
    [ValidFrom],
    [ValidTo],
    IIF(YEAR(ValidTo) = 9999, 1, 0) AS IsActual
FROM [dbo].[Department]
FOR SYSTEM_TIME BETWEEN '2021-01-01' AND '2021-12-31'
WHERE DeptId = 1
ORDER BY ValidFrom DESC;

/* Query using CONTAINED IN sub-clause */
SELECT [DeptID],
    [DeptName],
    [ValidFrom],
    [ValidTo]
FROM [dbo].[Department]
FOR SYSTEM_TIME CONTAINED IN ('2021-04-01', '2021-09-25')
WHERE DeptId = 1
ORDER BY ValidFrom DESC;

/* Query using ALL sub-clause */
SELECT [DeptID],
    [DeptName],
    [ValidFrom],
    [ValidTo],
    IIF(YEAR(ValidTo) = 9999, 1, 0) AS IsActual
FROM [dbo].[Department]
FOR SYSTEM_TIME ALL
ORDER BY [DeptID],
    [ValidFrom] DESC;
```

## Next steps

- [Temporal Tables](temporal-tables.md)
- [FROM (Transact-SQL)](../../t-sql/queries/from-transact-sql.md)
- [AT TIME ZONE (Transact-SQL)](../../t-sql/queries/at-time-zone-transact-sql.md)
- [Create a system-versioned temporal table](creating-a-system-versioned-temporal-table.md)
- [Modify data in a system-versioned temporal table](modifying-data-in-a-system-versioned-temporal-table.md)
- [Change the schema of a system-versioned temporal table](changing-the-schema-of-a-system-versioned-temporal-table.md)
- [Stop system-versioning on a system-versioned temporal table](stopping-system-versioning-on-a-system-versioned-temporal-table.md)
