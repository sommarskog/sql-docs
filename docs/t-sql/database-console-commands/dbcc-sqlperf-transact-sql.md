---
title: "DBCC SQLPERF (Transact-SQL)"
description: DBCC SQLPERF provides transaction log space usage statistics for all databases.
author: rwestMSFT
ms.author: randolphwest
ms.date: 12/05/2022
ms.service: sql
ms.subservice: t-sql
ms.topic: "language-reference"
f1_keywords:
  - "SQLPERF"
  - "DBCC_SQLPERF_TSQL"
  - "SQLPERF_TSQL"
  - "DBCC SQLPERF"
helpviewer_keywords:
  - "statistical information [SQL Server], transaction logs"
  - "transaction logs [SQL Server], space usage"
  - "space [SQL Server], transaction logs"
  - "DBCC SQLPERF statement"
dev_langs:
  - "TSQL"
---
# DBCC SQLPERF (Transact-SQL)

[!INCLUDE [SQL Server SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdb-asdbmi.md)]

Provides transaction log space usage statistics for all databases. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], it can also be used to reset wait and latch statistics.

**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later versions, and [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)] ([Preview in some regions](/azure/azure-sql/database/features-comparison?WT.mc_id=TSQL_GetItTag))

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
DBCC SQLPERF
(
     [ LOGSPACE ]
     | [ "sys.dm_os_latch_stats" , CLEAR ]
     | [ "sys.dm_os_wait_stats" , CLEAR ]
)
     [ WITH NO_INFOMSGS ]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### LOGSPACE

Returns the current size of the transaction log and the percentage of log space used for each database. Use this information to monitor the amount of space used in a transaction log.

> [!IMPORTANT]  
> For more information about space usage information for the transaction log starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], see the [Remarks](#remarks) section in this topic.

#### "sys.dm_os_latch_stats", CLEAR

Resets the latch statistics. For more information, see [sys.dm_os_latch_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md). This option isn't available in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

#### "sys.dm_os_wait_stats", CLEAR

Resets the wait statistics. For more information, see [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md). This option isn't available in [!INCLUDE[ssSDS](../../includes/sssds-md.md)].

#### WITH NO_INFOMSGS

Suppresses all informational messages that have severity levels from 0 through 10.

## Result sets

The following table describes the columns in the result set.

| Column name | Definition |
| --- | --- |
| **Database Name** | Name of the database for the log statistics displayed. |
| **Log Size (MB)** | Current size allocated to the log. This value is always smaller than the amount originally allocated for log space because the [!INCLUDE[ssDE](../../includes/ssde-md.md)] reserves a small amount of disk space for internal header information. |
| **Log Space Used (%)** | Percentage of the log file currently in use to store transaction log information. |
| **Status** | Status of the log file. Always 0. |

## Remarks

Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], use the [sys.dm_db_log_space_usage](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md) DMV instead of `DBCC SQLPERF(LOGSPACE)`, to return space usage information for the transaction log per database.

The transaction log records each transaction made in a database. For more information, see [The Transaction Log (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md) and [SQL Server Transaction Log Architecture and Management Guide](../../relational-databases/sql-server-transaction-log-architecture-and-management-guide.md).

## Permissions

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] requires **VIEW SERVER STATE** permission on the server to run `DBCC SQLPERF(LOGSPACE)`. To reset wait and latch statistics requires `ALTER SERVER STATE` permission on the server.

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] Premium and Business Critical tiers require the **VIEW DATABASE STATE** permission in the database. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] Standard, Basic, and General Purpose tiers require the [!INCLUDE[ssSDS](../../includes/sssds-md.md)] admin account. Reset wait and latch statistics aren't supported.

## Examples

### A. Display log space information for all databases

The following example displays `LOGSPACE` information for all databases contained in the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

```sql
DBCC SQLPERF (LOGSPACE);
GO
```

[!INCLUDE[ssResult](../../includes/ssresult-md.md)]

```output
Database Name Log Size (MB) Log Space Used (%) Status
------------- ------------- ------------------ -----------
master         3.99219      14.3469            0
tempdb         1.99219      1.64216            0
model          1.0          12.7953            0
msdb           3.99219      17.0132            0
AdventureWorks 19.554688    17.748701          0
```

### B. Reset wait statistics

The following example resets the wait statistics for the instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

```sql
DBCC SQLPERF ("sys.dm_os_wait_stats", CLEAR);
```

## See also

- [DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
- [sys.dm_os_latch_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-latch-stats-transact-sql.md)
- [sys.dm_os_wait_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)
- [sp_spaceused (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)
- [sys.dm_db_log_info (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-info-transact-sql.md)
- [sys.dm_db_log_space_usage (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-space-usage-transact-sql.md)
- [sys.dm_db_log_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md)
