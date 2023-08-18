---
title: DBCC CLEANTABLE (Transact-SQL)
description: DBCC CLEANTABLE reclaims space from dropped variable-length columns in tables or indexed views.
author: rwestMSFT
ms.author: randolphwest
ms.date: 04/18/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: "language-reference"
f1_keywords:
  - "CLEANTABLE_TSQL"
  - "DBCC_CLEANTABLE_TSQL"
  - "DBCC CLEANTABLE"
  - "CLEANTABLE"
helpviewer_keywords:
  - "disk space [SQL Server], reclaiming"
  - "reclaiming space"
  - "reallocating space"
  - "removing columns"
  - "DBCC CLEANTABLE statement"
  - "space [SQL Server], reclaiming"
  - "deleting columns"
  - "dropping columns"
dev_langs:
  - "TSQL"
---

# DBCC CLEANTABLE (Transact-SQL)

[!INCLUDE [SQL Server SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Reclaims space from dropped variable-length columns in tables or indexed views.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
DBCC CLEANTABLE
(
    { database_name | database_id | 0 }
    , { table_name | table_id | view_name | view_id }
    [ , batch_size ]
)
[ WITH NO_INFOMSGS ]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *database_name* | *database_id* | 0

The database in which the table to be cleaned belongs. If 0 is specified, the current database is used. Database names must follow the rules for [identifiers](../../relational-databases/databases/database-identifiers.md).

#### *table_name* | *table_id* | *view_name* | *view_id*

The table or indexed view to be cleaned.

#### *batch_size*

The number of rows processed per transaction. If not specified, the default value is `1000`. To avoid a long recovery period, `0` is not allowed.

#### WITH NO_INFOMSGS

Suppresses all informational messages.

## Remarks

`DBCC CLEANTABLE` reclaims space after a variable-length column is dropped. A variable-length column can be one of the following data types: **varchar**, **nvarchar**, **varchar(max)**, **nvarchar(max)**, **varbinary**, **varbinary(max)**, **text**, **ntext**, **image**, **sql_variant**, and **xml**. The command doesn't reclaim space after a fixed-length column is dropped.

If the dropped columns were stored in-row, `DBCC CLEANTABLE` reclaims space from the IN_ROW_DATA allocation unit of the table. If the columns were stored off-row, space is reclaimed from either the ROW_OVERFLOW_DATA or the LOB_DATA allocation unit depending on the data type of the dropped column. If reclaiming space from a ROW_OVERFLOW_DATA or LOB_DATA page results in an empty page, `DBCC CLEANTABLE` removes the page.

`DBCC CLEANTABLE` runs as one or more transactions. If a batch size isn't specified, the default size is `1000`. For some large tables, the length of the single transaction and the log space required may be too much. If a batch size is specified, the command runs in a series of transactions, each including the specified number of rows. `DBCC CLEANTABLE` can't be run as a transaction inside another transaction.

This operation is fully logged.

`DBCC CLEANTABLE` isn't supported for use on system tables, temporary tables, or the memory-optimized columnstore index portion of a table.

## Best practices

`DBCC CLEANTABLE` shouldn't be executed as a routine maintenance task. Instead, use `DBCC CLEANTABLE` after you make significant changes to variable-length columns in a table or indexed view and you need to immediately reclaim the unused space. Alternatively, you can rebuild the indexes on the table or view; however, doing so is a more resource-intensive operation.

## Result sets

`DBCC CLEANTABLE` returns:

```output
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```

## Permissions

Caller must own the table or indexed view, or be a member of the **sysadmin** fixed server role, the **db_owner** fixed database role, or the **db_ddladmin** fixed database role.

## Examples

### A. Use DBCC CLEANTABLE to reclaim space

The following example executes `DBCC CLEANTABLE` for the `Production.Document` table in the [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] sample database.

```sql
DBCC CLEANTABLE (AdventureWorks2022, 'Production.Document', 1000)
WITH NO_INFOMSGS;
GO
```

### B. Use DBCC CLEANTABLE and verifying results

The following example creates and populates a table with several variable-length columns. Two of the columns are then dropped and `DBCC CLEANTABLE` is run to reclaim the unused space. A query is run to verify the page counts and space used values before and after the `DBCC CLEANTABLE` command is executed.

```sql
USE AdventureWorks2022;
GO

IF OBJECT_ID('dbo.CleanTableTest', 'U') IS NOT NULL
    DROP TABLE dbo.CleanTableTest;
GO

CREATE TABLE dbo.CleanTableTest (
    FileName NVARCHAR(4000)
    , DocumentSummary NVARCHAR(max)
    , Document VARBINARY(max)
    );
GO

-- Populate the table with data from the Production.Document table.
INSERT INTO dbo.CleanTableTest
SELECT REPLICATE(FileName, 1000), DocumentSummary, Document
FROM Production.Document;
GO

-- Verify the current page counts and average space used in the dbo.CleanTableTest table.
DECLARE @db_id SMALLINT;
DECLARE @object_id INT;

SET @db_id = DB_ID(N'AdventureWorks2022');
SET @object_id = OBJECT_ID(N'AdventureWorks2022.dbo.CleanTableTest');

SELECT alloc_unit_type_desc
    , page_count
    , avg_page_space_used_in_percent
    , record_count
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL, 'Detailed');
GO

-- Drop two variable-length columns from the table.
ALTER TABLE dbo.CleanTableTest

DROP COLUMN FileName, Document;
GO

-- Verify the page counts and average space used in the dbo.CleanTableTest table
-- Notice that the values have not changed.
DECLARE @db_id SMALLINT;
DECLARE @object_id INT;

SET @db_id = DB_ID(N'AdventureWorks2022');
SET @object_id = OBJECT_ID(N'AdventureWorks2022.dbo.CleanTableTest');

SELECT alloc_unit_type_desc
    , page_count
    , avg_page_space_used_in_percent
    , record_count
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL, 'Detailed');
GO

-- Run DBCC CLEANTABLE.
DBCC CLEANTABLE (AdventureWorks2022, 'dbo.CleanTableTest');
GO

-- Verify the values in the dbo.CleanTableTest table after the DBCC CLEANTABLE command.
DECLARE @db_id SMALLINT;
DECLARE @object_id INT;

SET @db_id = DB_ID(N'AdventureWorks2022');
SET @object_id = OBJECT_ID(N'AdventureWorks2022.dbo.CleanTableTest');

SELECT alloc_unit_type_desc
    , page_count
    , avg_page_space_used_in_percent
    , record_count
FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL, 'Detailed');
GO
```

## See also

- [DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
- [sys.allocation_units (Transact-SQL)](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)
