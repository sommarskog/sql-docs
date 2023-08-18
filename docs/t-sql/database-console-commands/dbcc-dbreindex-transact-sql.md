---
title: "DBCC DBREINDEX (Transact-SQL)"
description: DBCC DBREINDEX rebuilds one or more indexes for a table in the specified database.
author: rwestMSFT
ms.author: randolphwest
ms.date: 12/05/2022
ms.service: sql
ms.subservice: t-sql
ms.topic: "language-reference"
f1_keywords:
  - "DBCC DBREINDEX"
  - "DBREINDEX_TSQL"
  - "DBREINDEX"
  - "DBCC_DBREINDEX_TSQL"
helpviewer_keywords:
  - "index rebuilding [SQL Server]"
  - "rebuilding indexes"
  - "dynamic index rebuilding [SQL Server]"
  - "DBCC DBREINDEX statement"
dev_langs:
  - "TSQL"
---
# DBCC DBREINDEX (Transact-SQL)

[!INCLUDE [SQL Server Azure SQL Managed Instance](../../includes/applies-to-version/sql-asdbmi.md)]

Rebuilds one or more indexes for a table in the specified database.

> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md) instead.

**Applies to**: [!INCLUDE[sql2008-md](../../includes/sql2008-md.md)] and later versions.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
DBCC DBREINDEX
(
    table_name
    [ , index_name [ , fillfactor ] ]
)
    [ WITH NO_INFOMSGS ]
```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *table_name*

The name of the table containing the specified index or indexes to rebuild. Table names must follow the rules for [identifiers](../../relational-databases/databases/database-identifiers.md)*.*

#### *index_name*

The name of the index to rebuild. Index names must comply with the rules for identifiers. If *index_name* is specified, *table_name* must be specified. If *index_name* isn't specified or is `' '`, all indexes for the table are rebuilt.

#### *fillfactor*

The percentage of space on each index page for storing data when the index is created or rebuilt. *fillfactor* replaces the fill factor when the index was created, becoming the new default for the index and for any other nonclustered indexes rebuilt, because a clustered index is rebuilt.  

When *fillfactor* is 0, `DBCC DBREINDEX` uses the fill factor value last specified for the index. This value is stored in the `sys.indexes` catalog view.  

If *fillfactor* is specified, *table_name* and *index_name* must be specified. If *fillfactor* isn't specified, the default fill factor, 100, is used. For more information, see [Specify Fill Factor for an Index](../../relational-databases/indexes/specify-fill-factor-for-an-index.md).

#### WITH NO_INFOMSGS

Suppresses all informational messages that have severity levels from 0 through 10.

## Remarks

`DBCC DBREINDEX` rebuilds an index for a table or all indexes defined for a table. By allowing an index to be rebuilt dynamically, indexes enforcing either PRIMARY KEY or UNIQUE constraints can be rebuilt without having to drop and re-create those constraints. This means that an index can be rebuilt without knowing the structure of a table or its constraints. This might occur after a bulk copy of data into the table.

`DBCC DBREINDEX` can rebuild all the indexes for a table in one statement. This is easier than coding multiple `DROP INDEX` and `CREATE INDEX` statements. Because the work is performed by one statement, `DBCC DBREINDEX` is automatically atomic, whereas individual `DROP INDEX` and `CREATE INDEX` statements must be included in a transaction to be atomic. Also, `DBCC DBREINDEX` offers more optimizations than individual `DROP INDEX` and `CREATE INDEX` statements.

Unlike `DBCC INDEXDEFRAG`, or `ALTER INDEX` with the `REORGANIZE` option, `DBCC DBREINDEX` is an offline operation. If a nonclustered index is being rebuilt, a shared lock is held on the table in question during the operation. This prevents modifications to the table. If the clustered index is being rebuilt, an exclusive table lock is held. This prevents any table access, therefore effectively making the table offline. To perform an index rebuild online, or to control the degree of parallelism during the index rebuild operation, use the `ALTER INDEX REBUILD` statement with the `ONLINE` option.

For more information about selecting a method to rebuild or reorganize an index, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

## Restrictions

`DBCC DBREINDEX` isn't supported for use on the following objects:

- System tables
- Spatial indexes
- memory-optimized columnstore indexes

## Result sets

Unless `NO_INFOMSGS` is specified (the table name must be specified), `DBCC DBREINDEX` always returns:

```sql
DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```

## Permissions

Caller must own the table, or be a member of the **sysadmin** fixed server role, the **db_owner** fixed database role, or the **db_ddladmin** fixed database role.

## Examples

### A. Rebuild an index

The following example rebuilds the `Employee_EmployeeID` clustered index with a fill factor of `80` on the `Employee` table in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database.

```sql
USE AdventureWorks2022;
GO
DBCC DBREINDEX ('HumanResources.Employee', PK_Employee_BusinessEntityID, 80);
GO
```

### B. Rebuild all indexes

The following example rebuilds all indexes on the `Employee` table in [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] by using a fill factor value of `70`.

```sql
USE AdventureWorks2022;
GO
DBCC DBREINDEX ('HumanResources.Employee', ' ', 70);
GO
```

## See also

- [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)
- [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)
- [DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)
- [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)
- [sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)
- [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)
