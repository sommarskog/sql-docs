---
title: "sys.sp_cleanup_temporal_history"
description: "Removes all rows from temporal history table that match configured HISTORY_RETENTION PERIOD within a single transaction."
author: markingmyname
ms.author: maghan
ms.reviewer: randolphwest
ms.date: 05/24/2023
ms.service: sql-database
ms.topic: conceptual
dev_langs:
  - "TSQL"
monikerRange: "= azuresqldb-current"
---
# sys.sp_cleanup_temporal_history (Transact-SQL)

[!INCLUDE [Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

Removes all rows from temporal history table that match configured HISTORY_RETENTION PERIOD within a single transaction.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
sp_cleanup_temporal_history
    [ @schema_name = ] N'schema_name'
    , [ @table_name = ] N'table_name'
    [ , [ @row_count = ] @row_count_var [ OUTPUT ] ]
```

## Arguments

#### [ @schema_name = ] N'*schema_name*'

The name of the temporal table for which retention cleanup is invoked.

#### [ @table_name = ] N'*table_name*'

The name of the schema that current temporal table belongs to.

#### [ @row_count = ] *@row_count_var* [ OUTPUT ]

The output parameter that returns number of deleted rows. If the history table has a clustered columnstore index, this parameter returns `0`.

## Remarks

This stored procedure can be used only with temporal tables that have finite retention period specified. Use this stored procedure only if you need to immediately clean all aged rows from the history table.

`sp_cleanup_temporal_history` can have a negative impact on the database log and I/O subsystem, as it deletes all eligible rows within the same transaction.

It is always recommended to rely on an internal background task for cleanup that removes aged rows with the minimal impact on the regular workloads and database in general.

## Permissions

Requires **db_owner** permissions.

## Example

```sql
DECLARE @rowcnt INT;

EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt OUTPUT;

SELECT @rowcnt;
```

## Next steps

- [Temporal tables retention policy](/azure/sql-database/sql-database-temporal-tables-retention-policy)
