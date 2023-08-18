---
title: "ALTER INDEX (Transact-SQL)"
description: ALTER INDEX (Transact-SQL)
author: rwestMSFT
ms.author: randolphwest
ms.reviewer: wiassaf, randolphwest
ms.date: 06/06/2023
ms.service: sql
ms.subservice: t-sql
ms.topic: reference
f1_keywords:
  - "ALTER INDEX"
  - "ALTER_INDEX_TSQL"
helpviewer_keywords:
  - "indexes [SQL Server], reorganizing"
  - "ALTER INDEX statement"
  - "indexes [SQL Server], disabling"
  - "online index operations"
  - "index reorganization [SQL Server]"
  - "ALLOW_ROW_LOCKS option"
  - "ALL keyword"
  - "reorganizing indexes"
  - "constraints [SQL Server], indexes"
  - "row locks [SQL Server]"
  - "index rebuilding [SQL Server]"
  - "rebuilding indexes"
  - "locking [SQL Server], indexes"
  - "partitioned indexes [SQL Server], rebuilding"
  - "defragmenting indexes"
  - "disabling indexes"
  - "XML indexes [SQL Server], modifying"
  - "index modifications [SQL Server]"
  - "indexes [SQL Server], modifying"
  - "index options [SQL Server]"
  - "modifying indexes"
  - "index disabling [SQL Server]"
  - "MAXDOP index option, ALTER INDEX statement"
  - "spatial indexes [SQL Server], modifying"
  - "indexes [SQL Server], options"
  - "ALLOW_PAGE_LOCKS option"
  - "page locks [SQL Server]"
  - "index rebuild [SQL Server]"
  - "index reorganize [SQL Server]"
dev_langs:
  - "TSQL"
monikerRange: ">=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current"
---

# ALTER INDEX (Transact-SQL)

[!INCLUDE [sql-asdb-asdbmi-asa-pdw](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Modifies an existing table or view index (rowstore, columnstore, or XML) by disabling, rebuilding, or reorganizing the index; or by setting options on the index.

:::image type="icon" source="../../includes/media/topic-link-icon.svg" border="false"::: [Transact-SQL syntax conventions](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)

## Syntax

```syntaxsql
-- Syntax for SQL Server and Azure SQL Database

ALTER INDEX { index_name | ALL } ON <object>
{
      REBUILD {
            [ PARTITION = ALL ] [ WITH ( <rebuild_index_option> [ ,...n ] ) ]
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> ) [ ,...n ] ]
      }
    | DISABLE
    | REORGANIZE  [ PARTITION = partition_number ] [ WITH ( <reorganize_option>  ) ]
    | SET ( <set_index_option> [ ,...n ] )
    | RESUME [WITH (<resumable_index_options>,[...n])]
    | PAUSE
    | ABORT
}
[ ; ]

<object> ::=
{
    { database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }
}

<rebuild_index_option> ::=
{
      PAD_INDEX = { ON | OFF }
    | FILLFACTOR = fillfactor
    | SORT_IN_TEMPDB = { ON | OFF }
    | IGNORE_DUP_KEY = { ON | OFF }
    | STATISTICS_NORECOMPUTE = { ON | OFF }
    | STATISTICS_INCREMENTAL = { ON | OFF }
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }
    | RESUMABLE = { ON | OFF }
    | MAX_DURATION = <time> [MINUTES}
    | ALLOW_ROW_LOCKS = { ON | OFF }
    | ALLOW_PAGE_LOCKS = { ON | OFF }
    | MAXDOP = max_degree_of_parallelism
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]
    | XML_COMPRESSION = { ON | OFF }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]}

<single_partition_rebuild_index_option> ::=
{
      SORT_IN_TEMPDB = { ON | OFF }
    | MAXDOP = max_degree_of_parallelism
    | RESUMABLE = { ON | OFF }
    | MAX_DURATION = <time> [MINUTES}
    | DATA_COMPRESSION = { NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }
    | XML_COMPRESSION = { ON | OFF }
    | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }
}

<reorganize_option>::=
{
       LOB_COMPACTION = { ON | OFF }
    |  COMPRESS_ALL_ROW_GROUPS =  { ON | OFF}
}

<set_index_option>::=
{
      ALLOW_ROW_LOCKS = { ON | OFF }
    | ALLOW_PAGE_LOCKS = { ON | OFF }
    | OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }
    | IGNORE_DUP_KEY = { ON | OFF }
    | STATISTICS_NORECOMPUTE = { ON | OFF }
    | COMPRESSION_DELAY = { 0 | delay [Minutes] }
}

<resumable_index_option> ::=
 {
    MAXDOP = max_degree_of_parallelism
    | MAX_DURATION =<time> [MINUTES]
    | <low_priority_lock_wait>
 }

<low_priority_lock_wait>::=
{
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,
                          ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )
}

```

```syntaxsql
-- Syntax for Azure Synapse Analytics and Parallel Data Warehouse

ALTER INDEX { index_name | ALL }
    ON   [ schema_name. ] table_name
{
      REBUILD {
            [ PARTITION = ALL [ WITH ( <rebuild_index_option> ) ] ]
          | [ PARTITION = partition_number [ WITH ( <single_partition_rebuild_index_option> )] ]
      }
    | DISABLE
    | REORGANIZE [ PARTITION = partition_number ]
}
[;]

<rebuild_index_option> ::=
{
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]
    | XML_COMPRESSION = { ON | OFF }
        [ ON PARTITIONS ( {<partition_number> [ TO <partition_number>] } [ , ...n ] ) ]
}

<single_partition_rebuild_index_option> ::=
{
    DATA_COMPRESSION = { COLUMNSTORE | COLUMNSTORE_ARCHIVE }
    | XML_COMPRESSION = { ON | OFF }
}

```

[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## Arguments

#### *index_name*

The name of the index. Index names must be unique within a table or view but don't have to be unique within a database. Index names must follow the rules of [identifiers](../../relational-databases/databases/database-identifiers.md).

#### ALL

Specifies all indexes associated with the table or view regardless of the index type. Specifying ALL causes the statement to fail if one or more indexes are in an offline or read-only filegroup or the specified operation isn't allowed on one or more index types. The following table lists the index operations and disallowed index types.

|Using the keyword ALL with this operation|Fails if the table has one or more|
|----------------------------------------|----------------------------------------|
|REBUILD WITH ONLINE = ON|XML index<br /><br />Spatial index<br /><br />Columnstore index: **Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]|
|REBUILD PARTITION = *partition_number*|Nonpartitioned index, XML index, spatial index, or disabled index|
|REORGANIZE|Indexes with ALLOW_PAGE_LOCKS set to OFF|
|REORGANIZE PARTITION = *partition_number*|Nonpartitioned index, XML index, spatial index, or disabled index|
|IGNORE_DUP_KEY = ON|XML index<br /><br />Spatial index<br /><br />Columnstore index: **Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]|
|ONLINE = ON|XML index<br /><br />Spatial index<br /><br />Columnstore index: **Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]|
|RESUMABLE = ON| Resumable indexes not supported with **All** keyword. <br /><br />**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)] |

> [!WARNING]  
> For more detailed information about index operations that can be performed online, see [Guidelines for Online Index Operations](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

If ALL is specified with PARTITION = *partition_number*, all indexes must be aligned. This means that they're partitioned based on equivalent partition functions. Using ALL with PARTITION causes all index partitions with the same *partition_number* to be rebuilt or reorganized. For more information about partitioned indexes, see [Partitioned Tables and Indexes](../../relational-databases/partitions/partitioned-tables-and-indexes.md).

#### *database_name*

The name of the database.

#### *schema_name*

The name of the schema to which the table or view belongs.

#### *table_or_view_name*

The name of the table or view associated with the index. To display a report of the indexes on an object, use the [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) catalog view.

[!INCLUDE[ssSDS](../../includes/sssds-md.md)] supports the three-part name format database_name.[schema_name].table_or_view_name when the database_name is the current database or the database_name is tempdb and the table_or_view_name starts with #.

#### REBUILD [ WITH (\<rebuild_index_option> [ ,... *n*]) ]

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Specifies the index will be rebuilt using the same columns, index type, uniqueness attribute, and sort order. This clause is equivalent to [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md). `REBUILD` enables a disabled index. Rebuilding a clustered index doesn't rebuild associated nonclustered indexes unless the keyword ALL is specified. If index options aren't specified, the existing index option values stored in [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) are applied. For any index option whose value isn't stored in `sys.indexes`, the default indicated in the argument definition of the option applies.

If ALL is specified and the underlying table is a heap, the `REBUILD` operation has no effect on the table. Any nonclustered indexes associated with the table are rebuilt.

The `REBUILD` operation can be minimally logged if the database recovery model is set to either bulk-logged or simple.

> [!NOTE]  
> When you rebuild a primary XML index, the underlying user table is unavailable for the duration of the index operation.

For columnstore indexes, the `REBUILD` operation:

- Doesn't use the sort order.
- Acquires an exclusive lock on the table or partition while the `REBUILD` occurs.  The data is "offline" and unavailable during the `REBUILD`, even when using NOLOCK, Read Committed Snapshot isolation (RCSI), or Snapshot isolation (SI).
- Recompresses all data into the columnstore. Two copies of the columnstore index exist while the `REBUILD` is taking place. When the `REBUILD` is finished, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deletes the original columnstore index.

For more information, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

#### PARTITION

Specifies that only one partition of an index will be rebuilt or reorganized. PARTITION can't be specified if *index_name* isn't a partitioned index.

PARTITION = ALL rebuilds all partitions.

> [!WARNING]  
> Creating and rebuilding nonaligned indexes on a table with more than 1,000 partitions is possible, but is not supported. Doing so may cause degraded performance or excessive memory consumption during these operations. Microsoft recommends using only aligned indexes when the number of partitions exceed 1,000.

***partition_number***

The partition number of a partitioned index that is to be rebuilt or reorganized. *partition_number* is a constant expression that can reference variables. These include user-defined type variables or functions and user-defined functions, but can't reference a [!INCLUDE[tsql](../../includes/tsql-md.md)] statement. *partition_number* must exist or the statement fails.

**WITH (<single_partition_rebuild_index_option>)**

`SORT_IN_TEMPDB`, `MAXDOP`, `DATA_COMPRESSION`, and `XML_COMPRESSION` are the options that can be specified when you `REBUILD` a single partition `(PARTITION = partition_number)`. XML indexes can't be specified in a single partition `REBUILD` operation.

#### DISABLE

Marks the index as disabled and unavailable for use by the [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Any index can be disabled. The index definition of a disabled index remains in the system catalog with no underlying index data. Disabling a clustered index prevents user access to the underlying table data. To enable an index, use `ALTER INDEX REBUILD` or `CREATE INDEX WITH DROP_EXISTING`. For more information, see [Disable Indexes and Constraints](../../relational-databases/indexes/disable-indexes-and-constraints.md) and [Enable Indexes and Constraints](../../relational-databases/indexes/enable-indexes-and-constraints.md).

#### REORGANIZE a rowstore index

For rowstore indexes, REORGANIZE specifies to reorganize the index leaf level. The REORGANIZE operation is:

- Always performed online. This means long-term blocking table locks aren't held and queries or updates to the underlying table can continue during the `ALTER INDEX REORGANIZE` transaction.
- Not allowed for a disabled index.
- Not allowed when ALLOW_PAGE_LOCKS is set to OFF.
- Not rolled back when it is performed within a transaction and the transaction is rolled back.

> [!NOTE]  
> When `ALTER INDEX REORGANIZE` uses explicit transactions (for example, `ALTER INDEX` inside a `BEGIN TRAN ... COMMIT/ROLLBACK`) instead of the default implicit transaction mode, the locking behavior of `REORGANIZE` becomes more restrictive, potentially causing blocking. For more information about implicit transactions, see [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).

For more information, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

#### REORGANIZE WITH ( LOB_COMPACTION = { ON | OFF } )

Applies to rowstore indexes.

LOB_COMPACTION = ON

- Specifies to compact all pages that contain data of these large object (LOB) data types: **image**, **text**, **ntext**, **varchar(max)**, **nvarchar(max)**, **varbinary(max)**, and **xml**. Compacting this data can reduce the data size on disk.
- For a clustered index, this compacts all LOB columns that are contained in the table.
- For a nonclustered index, this compacts all LOB columns that are nonkey (included) columns in the index.
- `REORGANIZE ALL` performs LOB_COMPACTION on all indexes. For each index, this compacts all LOB columns in the clustered index, underlying table, or included columns in a nonclustered index.

LOB_COMPACTION = OFF

- Pages that contain large object data aren't compacted.
- OFF has no effect on a heap.

#### REORGANIZE a columnstore index

For columnstore indexes, `REORGANIZE` compresses each CLOSED delta rowgroup into the columnstore as a compressed rowgroup. The `REORGANIZE` operation is always performed online. This means long-term blocking table locks aren't held and queries or updates to the underlying table can continue during the `ALTER INDEX REORGANIZE` transaction. For more information, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

- REORGANIZE isn't required in order to move CLOSED delta rowgroups into compressed rowgroups. The background tuple-mover (TM) process wakes up periodically  to compress CLOSED delta rowgroups. We recommend using REORGANIZE when tuple-mover is falling behind. REORGANIZE can compress rowgroups more aggressively.
- To compress all OPEN and CLOSED rowgroups, see the `REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS)` option in this section.

For columnstore indexes in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], REORGANIZE performs the following additional defragmentation optimizations online:

- Physically removes rows from a rowgroup when 10% or more of the rows have been logically deleted. The deleted bytes are reclaimed on the physical media. For example, if a compressed row group of 1 million rows has 100,000 rows deleted, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will remove the deleted rows and recompress the rowgroup with 900k rows. It saves on the storage by removing deleted rows.

- Combines one or more compressed rowgroups to increase rows per rowgroup up to the maximum of 1,048,576 rows. For example, if you bulk import 5 batches of 102,400 rows you'll get 5 compressed rowgroups. If you run REORGANIZE, these rowgroups will get merged into 1 compressed rowgroup of size 512,000 rows. This assumes there were no dictionary size or memory limitations.

- For rowgroups in which 10% or more of the rows  have been logically deleted, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will try to combine this rowgroup with one or more rowgroups. For example, rowgroup 1 is compressed with 500,000 rows and rowgroup 21 is compressed with the maximum of 1,048,576 rows. Rowgroup 21 has 60% of the rows deleted which leaves 409,830 rows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] favors combining these two rowgroups to compress a new rowgroup that has 909,830 rows.

#### REORGANIZE WITH ( COMPRESS_ALL_ROW_GROUPS = { ON | OFF } )

Applies to columnstore indexes.

**Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

COMPRESS_ALL_ROW_GROUPS provides a way to force OPEN or CLOSED delta rowgroups into the columnstore. With this option, it isn't necessary to rebuild the columnstore index to empty the delta rowgroups.  This, combined with the other remove and merge defragmentation features makes it no longer necessary to rebuild the index in most situations.

- ON forces all rowgroups into the columnstore, regardless of size and state (CLOSED or OPEN).
- OFF forces all CLOSED rowgroups into the columnstore.

For more information, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

#### SET ( \<set_index option\> [ ,... *n*] )

Specifies index options without rebuilding or reorganizing the index. SET can't be specified for a disabled index.

#### PAD_INDEX = { ON | OFF }

Specifies index padding. The default is OFF.

ON  

The percentage of free space that is specified by `FILLFACTOR` is applied to the intermediate-level pages of the index. If `FILLFACTOR` isn't specified at the same time `PAD_INDEX` is set to ON, the fill factor value stored in [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) is used.

OFF or *fillfactor* isn't specified

The intermediate-level pages are filled to near capacity. This leaves sufficient space for at least one row of the maximum size that the index can have, based on the set of keys on the intermediate pages.

For more information, see [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).

#### FILLFACTOR = *fillfactor*

Specifies a percentage that indicates how full the [!INCLUDE[ssDE](../../includes/ssde-md.md)] should make the leaf level of each index page during index creation or alteration. The value for _fillfactor_ must be an integer value from 1 to 100. The default is 0. Fill factor values 0 and 100 are the same in all respects.

An explicit `FILLFACTOR` setting applies only when the index is first created or rebuilt. The [!INCLUDE[ssDE](../../includes/ssde-md.md)] doesn't dynamically keep the specified percentage of empty space in the pages. For more information, see [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).

To view the fill factor setting, use `fill_factor` in `sys.indexes`.

> [!IMPORTANT]  
> Creating or altering a clustered index with a `FILLFACTOR` value affects the amount of storage space the data occupies, because the [!INCLUDE[ssDE](../../includes/ssde-md.md)] redistributes the data when it creates the clustered index.

#### SORT_IN_TEMPDB = { ON | OFF }

Specifies whether to store the sort results in **tempdb**. The default is OFF except for Azure SQL Database Hyperscale. For all index rebuild operations in Hyperscale, `SORT_IN_TEMPDB` is always ON, regardless of the option specified unless resumable index rebuild is used.

ON  
The intermediate sort results that are used to build the index are stored in **tempdb**. If **tempdb** is on a different set of disks than the user database, this may reduce the time needed to create an index. However, this increases the amount of disk space that is used during the index build.

OFF  
The intermediate sort results are stored in the same database as the index.

If a sort operation isn't required, or if the sort can be performed in memory, the `SORT_IN_TEMPDB` option is ignored.

For more information, see [SORT_IN_TEMPDB Option For Indexes](../../relational-databases/indexes/sort-in-tempdb-option-for-indexes.md).

#### IGNORE_DUP_KEY = { ON | OFF }
Specifies the error response when an insert operation attempts to insert duplicate key values into a unique index. The `IGNORE_DUP_KEY` option applies only to insert operations after the index is created or rebuilt. The default is OFF.

ON  
A warning message will occur when duplicate key values are inserted into a unique index. Only the rows violating the uniqueness constraint will fail.

OFF  
An error message will occur when duplicate key values are inserted into a unique index. The entire INSERT operation will be rolled back.

 `IGNORE_DUP_KEY` can't be set to ON for indexes created on a view, non-unique indexes, XML indexes, spatial indexes, and filtered indexes.

To view `IGNORE_DUP_KEY`, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).

In backward compatible syntax, `WITH IGNORE_DUP_KEY` is equivalent to `WITH IGNORE_DUP_KEY = ON`.

#### STATISTICS_NORECOMPUTE = { ON | OFF }
Specifies whether distribution statistics are recomputed. The default is OFF.

ON  
Out-of-date statistics aren't automatically recomputed.

OFF  
Automatic statistics updating are enabled.

To restore automatic statistics updating, set the `STATISTICS_NORECOMPUTE` to OFF, or execute `UPDATE STATISTICS` without the `NORECOMPUTE` clause.

> [!IMPORTANT]  
> Disabling automatic recomputation of distribution statistics may prevent the Query Optimizer from picking optimal execution plans for queries that involve the table.

#### STATISTICS_INCREMENTAL = { ON | OFF }

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

When **ON**, the statistics created are per partition statistics. When **OFF**, the statistics tree is dropped and [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recomputes the statistics. The default is **OFF**.

If per partition statistics aren't supported the option is ignored and a warning is generated. Incremental stats aren't supported for following statistics types:

- Statistics created with indexes that aren't partition-aligned with the base table
- Statistics created on availability group readable secondary databases
- Statistics created on read-only databases
- Statistics created on filtered indexes
- Statistics created on views
- Statistics created on internal tables
- Statistics created with spatial indexes or XML indexes

#### ONLINE = { ON | OFF } \<as applies to rebuild_index_option>

Specifies whether underlying tables and associated indexes are available for queries and data modification during the index operation. The default is OFF.

For an XML index or spatial index, only `ONLINE = OFF` is supported, and if ONLINE is set to ON an error is raised.

> [!IMPORTANT]  
> Online index operations are not available in every edition of [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For a list of features that are supported by the editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see:
>  
>- [Editions and supported features of SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)
>- [Editions and supported features of SQL Server 2017](../../sql-server/editions-and-components-of-sql-server-2017.md)
>- [Editions and supported features of SQL Server 2019](../../sql-server/editions-and-components-of-sql-server-2019.md)

ON  
Long-term table locks aren't held during the index operation. During the main phase of the index operation, only an Intent Share (IS) lock is held on the source table. This allows queries or updates to the underlying table and indexes to continue. At the start of the operation, a Shared (S) lock is very briefly held on the source object. At the end of the operation, an S lock is very briefly held on the source if a nonclustered index is being created. A Schema Modification (Sch-M) lock is acquired when a clustered index is created or dropped online and when a clustered or nonclustered index is being rebuilt. ONLINE can't be set to ON when an index is being created on a local temporary table.

OFF  
Table locks are applied during the index operation. An offline index operation that creates, rebuilds, or drops a clustered, spatial, or XML index, or rebuilds or drops a nonclustered index, acquires a Schema modification (Sch-M) lock on the table. This prevents all user access to the underlying table during the operation. An offline index operation that creates a nonclustered index acquires a Shared (S) lock on the table. This prevents updates to the underlying table but allows read operations, such as SELECT statements.

For more information, see [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).

Indexes, including indexes on global temp tables, can be rebuilt online except for the following cases:

- XML index
- Index on a local temp table
- Initial unique clustered index on a view
- Columnstore indexes
- Clustered index, if the underlying table contains LOB data types (**image**, **ntext**, **text**) and spatial data types
- **varchar(max)** and **varbinary(max)** columns can't be part of an index. In [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], when a table contains **varchar(max)** or **varbinary(max)** columns, a clustered index containing other columns can be built or rebuilt using the `ONLINE` option. [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)] doesn't permit the `ONLINE` option when the base table contains **varchar(max)** or **varbinary(max)** columns

For more information, see [How Online Index Operations Work](../../relational-databases/indexes/how-online-index-operations-work.md).

#### RESUMABLE = { ON | OFF}

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Specifies whether an online index operation is resumable.

ON  
Index operation is resumable.

OFF  
Index operation isn't resumable.

#### MAX_DURATION = *time* [**MINUTES**] used with `RESUMABLE = ON` (requires `ONLINE = ON`)

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Indicates time (an integer value specified in minutes) that a resumable online index operation is executed before being paused.

> [!IMPORTANT]  
> For more detailed information about index operations that can be performed online, see [Guidelines for Online Index Operations](../../relational-databases/indexes/guidelines-for-online-index-operations.md).

> [!NOTE]  
> Resumable online index rebuilds are not supported on columnstore indexes.

#### ALLOW_ROW_LOCKS = { ON | OFF }

Specifies whether row locks are allowed. The default is ON.

ON  
Row locks are allowed when accessing the index. The [!INCLUDE[ssDE](../../includes/ssde-md.md)] determines when row locks are used.

OFF  
Row locks aren't used.

#### ALLOW_PAGE_LOCKS = { ON | OFF }

Specifies whether page locks are allowed. The default is ON.

ON  
Page locks are allowed when you access the index. The [!INCLUDE[ssDE](../../includes/ssde-md.md)] determines when page locks are used.

OFF  
Page locks aren't used.

> [!NOTE]  
> An index cannot be reorganized when ALLOW_PAGE_LOCKS is set to OFF.

#### OPTIMIZE_FOR_SEQUENTIAL_KEY = { ON | OFF }

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[sql-server-2019](../../includes/sssql19-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Specifies whether or not to optimize for last-page insert contention. The default is OFF. For more information, see [Sequential Keys](./create-index-transact-sql.md#sequential-keys).

#### MAXDOP = max_degree_of_parallelism

Overrides the **max degree of parallelism** configuration option during the index operation. For more information, see [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Use MAXDOP to limit the number of processors used in a parallel plan execution. The maximum is 64 processors.

> [!IMPORTANT]  
> Although the MAXDOP option is syntactically supported for all XML indexes, for a spatial index or a primary XML index, `ALTER INDEX` currently uses only a single processor.

*max_degree_of_parallelism* can be:

 1  
Suppresses parallel plan generation.

 \>1  
Restricts the maximum number of processors used in a parallel index operation to the specified number.

0 (default)  
Uses the actual number of processors or fewer based on the current system workload.

For more information, see [Configure Parallel Index Operations](../../relational-databases/indexes/configure-parallel-index-operations.md).

> [!NOTE]  
> Parallel index operations are not available in every edition of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. For a list of features that are supported by the editions of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], see [Editions and supported features of SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md).

#### COMPRESSION_DELAY = { 0 | *duration [Minutes]* }

**Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)])

For a disk-based table, delay specifies the minimum number of minutes a delta rowgroup in the CLOSED state must remain in the delta rowgroup before [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] can compress it into the compressed rowgroup. Since disk-based tables don't track insert and update times on individual rows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] applies the delay to delta rowgroups in the CLOSED state.

The default is 0 minutes.

For recommendations on when to use COMPRESSION_DELAY, see [Get started with Columnstore for real time operational analytics](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md).

#### DATA_COMPRESSION

Specifies the data compression option for the specified index, partition number, or range of partitions. The options are as follows:

NONE  
Index or specified partitions aren't compressed. This doesn't apply to columnstore indexes.

ROW  
Index or specified partitions are compressed by using row compression. This doesn't apply to columnstore indexes.

PAGE  
Index or specified partitions are compressed by using page compression. This doesn't apply to columnstore indexes.

COLUMNSTORE

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Applies only to columnstore indexes, including both nonclustered columnstore and clustered columnstore indexes. COLUMNSTORE specifies to decompress the index or specified partitions that are compressed with the COLUMNSTORE_ARCHIVE option. When the data is restored, it will continue to be compressed with the columnstore compression that is used for all columnstore indexes.

COLUMNSTORE_ARCHIVE

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Applies only to columnstore indexes, including both nonclustered columnstore and clustered columnstore indexes. COLUMNSTORE_ARCHIVE will further compress the specified partition to a smaller size. This can be used for archival, or for other situations that require a smaller storage size and can afford more time for storage and retrieval.

For more information about compression, see [Data Compression](../../relational-databases/data-compression/data-compression.md).

#### XML_COMPRESSION

**Applies to**: [!INCLUDE[sssql22-md](../../includes/sssql22-md.md)] and later versions, [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], and [!INCLUDE [ssazuremi](../../includes/ssazuremi_md.md)].

Specifies the XML compression option for the specified index that contains one or more **xml** data type columns. The options are as follows:

ON  
Index or specified partitions are compressed by using XML compression.

OFF  
Index or specified partitions are not compressed.

#### ON PARTITIONS ( { \<partition_number_expression> | \<range\> } [,...n] )

Specifies the partitions to which the DATA_COMPRESSION or XML_COMPRESSION settings apply. If the index isn't partitioned, the ON PARTITIONS argument will generate an error. If the ON PARTITIONS clause isn't provided, the DATA_COMPRESSION or XML_COMPRESSION option applies to all partitions of a partitioned index.

`<partition_number_expression>` can be specified in the following ways:

- Provide the number for a partition, for example: `ON PARTITIONS (2)`.
- Provide the partition numbers for several individual partitions separated by commas, for example: `ON PARTITIONS (1, 5)`.
- Provide both ranges and individual partitions: `ON PARTITIONS (2, 4, 6 TO 8)`.

`<range>` can be specified as partition numbers separated by the word TO, for example: `ON PARTITIONS (6 TO 8)`.

To set different types of data compression for different partitions, specify the DATA_COMPRESSION option more than once, for example:

```sql
REBUILD WITH
(
DATA_COMPRESSION = NONE ON PARTITIONS (1),
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)
);
```

You can also specify the XML_COMPRESSION option more than once, for example:

```sql
REBUILD WITH
(
  XML_COMPRESSION = OFF ON PARTITIONS (1),
  XML_COMPRESSION = ON ON PARTITIONS (2, 4, 6 TO 8),
  XML_COMPRESSION = OFF ON PARTITIONS (3, 5)
);
```

#### ONLINE = { ON | OFF } \<as applies to single_partition_rebuild_index_option\>

Specifies whether an index or an index partition of an underlying table can be rebuilt online or offline. If `REBUILD ... ONLINE = ON` is performed, the data in this table is available for queries and data modification during the index operation. The default is **OFF**.

ON  
Long-term table locks aren't held during the index operation. During the main phase of the index operation, only an Intent Share (IS) lock is held on the source  table. A Schema Stability (Sch-S) lock on the table is required when starting the index rebuild, and a Schema Modification (Sch-M) lock is required on the table at the end of the online index rebuild. Although both metadata locks are short in duration, the Sch-M lock especially must wait for all blocking transactions to be completed. During the wait time, the Sch-M lock blocks all other transactions that wait behind this lock when accessing the same table.

> [!NOTE]  
> Online index rebuild can set the `low_priority_lock_wait` options, see [WAIT_AT_LOW_PRIORITY with online index operations](#wait-at-low-priority).

OFF  
Table locks are applied during the index operation. This prevents all user access to the underlying table during the operation.

#### RESUME

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Resume an index operation that is paused manually or due to a failure.

MAX_DURATION used with `RESUMABLE = ON`

The time (an integer value specified in minutes) that the resumable online index operation is executed after being resumed. Once the time expires, the resumable operation is paused if it's still running.

WAIT_AT_LOW_PRIORITY used with `RESUMABLE = ON` and `ONLINE = ON`.

Resuming an online index rebuild after a pause has to wait for blocking operations on this table. `WAIT_AT_LOW_PRIORITY` indicates that the online index rebuild operation will wait for low priority locks, allowing other operations to proceed while the online index build operation is waiting. Omitting the `WAIT_AT_LOW_PRIORITY` option is equivalent to `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`. For more information, see [WAIT_AT_LOW_PRIORITY](alter-index-transact-sql.md#wait-at-low-priority).

#### PAUSE

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Pause a resumable online index rebuild operation.

#### ABORT

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Abort a running or paused index operation that was declared as resumable. You must explicitly execute an `ABORT` command to terminate a resumable index rebuild operation. Failure or pausing a resumable index operation doesn't terminate its execution; rather, it leaves the operation in an indefinite pause state.

## Remarks

`ALTER INDEX` can't be used to repartition an index or move it to a different filegroup. This statement can't be used to modify the index definition, such as adding or deleting columns or changing the column order. Use `CREATE INDEX` with the `DROP_EXISTING` clause to perform these operations.

When an option isn't explicitly specified, the current setting is applied. For example, if a `FILLFACTOR` setting isn't specified in the `REBUILD` clause, the fill factor value stored in the system catalog will be used during the rebuild process. To view the current index option settings, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).

The values for `ONLINE`, `MAXDOP`, and `SORT_IN_TEMPDB` aren't stored in the system catalog. Unless specified in the index statement, the default value for the option is used.

On multiprocessor computers, just like other queries do, `ALTER INDEX REBUILD` automatically uses more processors to perform the scan and sort operations that are associated with modifying the index. When you run `ALTER INDEX REORGANIZE`, with or without LOB_COMPACTION, the **max degree of parallelism** value is a single threaded operation. For more information, see [Configure Parallel Index Operations](../../relational-databases/indexes/configure-parallel-index-operations.md).

> [!IMPORTANT]  
> An index cannot be reorganized or rebuilt if the filegroup in which it is located is offline or set to read-only. When the keyword ALL is specified and one or more indexes are in an offline or read-only filegroup, the statement fails.

## <a id="rebuilding-indexes"></a> Rebuilding indexes

Rebuilding an index drops and re-creates the index. This removes fragmentation, reclaims disk space by compacting the pages based on the specified or existing fill factor setting, and reorders the index rows in contiguous pages. When ALL is specified, all indexes on the table are dropped and rebuilt in a single transaction. Foreign key constraints don't have to be dropped in advance. When indexes with 128 extents or more are rebuilt, the [!INCLUDE[ssDE](../../includes/ssde-md.md)] defers the actual page deallocations, and their associated locks, until after the transaction commits.

For more information, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

## <a id="reorganizing-indexes"></a> Reorganizing indexes

Reorganizing an index uses minimal system resources. It defragments the leaf level of clustered and nonclustered indexes on tables and views by physically reordering the leaf-level pages to match the logical, left to right, order of the leaf nodes. Reorganizing also compacts the index pages. Compaction is based on the existing fill factor value.

When `ALL` is specified, relational indexes, both clustered and nonclustered, and XML indexes on the table are reorganized. Some restrictions apply when specifying ALL, refer to the definition for ALL in the Arguments section of this article.

For more information, see [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md).

> [!IMPORTANT]  
> For an [!INCLUDE[ssazuresynapse-md](../../includes/ssazuresynapse-md.md)] table with an ordered clustered columnstore index, `ALTER INDEX REORGANIZE` does not re-sort the data. To resort the data use `ALTER INDEX REBUILD`.

## <a id="disabling-indexes"></a> Disabling indexes

Disabling an index prevents user access to the index, and for clustered indexes, to the underlying table data. The index definition remains in the system catalog. Disabling a nonclustered index or clustered index on a view physically deletes the index data. Disabling a clustered index prevents access to the data, but the data remains unmaintained in the B-tree until the index is dropped or rebuilt. To view the status of an enabled or disabled index, query the `is_disabled` column in the `sys.indexes` catalog view.

[!INCLUDE [sql-b-tree](../../includes/sql-b-tree.md)]

If a table is in a transactional replication publication, you can't disable any indexes that are associated with primary key columns. These indexes are required by replication. To disable an index, you must first drop the table from the publication. For more information, see [Publish Data and Database Objects](../../relational-databases/replication/publish/publish-data-and-database-objects.md).

Use the `ALTER INDEX REBUILD` statement or the `CREATE INDEX WITH DROP_EXISTING` statement to enable the index. Rebuilding a disabled clustered index can't be performed with the ONLINE option set to ON. For more information, see [Disable Indexes and Constraints](../../relational-databases/indexes/disable-indexes-and-constraints.md).

## Setting options

You can set the options `ALLOW_ROW_LOCKS`, `ALLOW_PAGE_LOCKS`, `OPTIMIZE_FOR_SEQUENTIAL_KEY`, `IGNORE_DUP_KEY` and `STATISTICS_NORECOMPUTE` for a specified index without rebuilding or reorganizing that index. The modified values are immediately applied to the index. To view these settings, use `sys.indexes`. For more information, see [Set Index Options](../../relational-databases/indexes/set-index-options.md).

### Row and page locks options

When `ALLOW_ROW_LOCKS = ON` and `ALLOW_PAGE_LOCK = ON`, row-level, page-level, and table-level locks are allowed when you access the index. The [!INCLUDE[ssDE](../../includes/ssde-md.md)] chooses the appropriate lock and can escalate the lock from a row or page lock to a table lock.

When `ALLOW_ROW_LOCKS = OFF` and `ALLOW_PAGE_LOCK = OFF`, only a table-level lock is allowed when you access the index.

If ALL is specified when the row or page lock options are set, the settings are applied to all indexes. When the underlying table is a heap, the settings are applied in the following ways:

|Option|Details|
|------|-------|
|ALLOW_ROW_LOCKS = ON or OFF|To the heap and any associated nonclustered indexes.|
|ALLOW_PAGE_LOCKS = ON|To the heap and any associated nonclustered indexes.|
|ALLOW_PAGE_LOCKS = OFF|Fully to the nonclustered indexes. This means that all page locks aren't allowed on the nonclustered indexes. On the heap, only the shared (S), update (U) and exclusive (X) locks for the page aren't allowed. The [!INCLUDE[ssDE](../../includes/ssde-md.md)] can still acquire an intent page lock (IS, IU or IX) for internal purposes.|

## <a id="online-index-operations"></a> Online index operations

When rebuilding an index and the ONLINE option is set to ON, the underlying objects, the tables and associated indexes, are available for queries and data modification. You can also rebuild online a portion of an index residing on a single partition. Exclusive table locks are held only for a very short amount of time during the alteration process.

Reorganizing an index is always performed online. The process doesn't hold locks long term and, therefore, doesn't block queries or updates that are running.

You can perform concurrent online index operations on the same table or table partition only when doing the following:

- Creating multiple nonclustered indexes.
- Reorganizing different indexes on the same table.
- Reorganizing different indexes while rebuilding nonoverlapping indexes on the same table.

All other online index operations performed at the same time fail. For example, you can't rebuild two or more indexes on the same table concurrently, or create a new index while rebuilding an existing index on the same table.

For more information, see [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).

### <a id="resumable-indexes"></a> Resumable index operations

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

Online index rebuild is specified as resumable using the `RESUMABLE = ON` option.

- The `RESUMABLE` option isn't persisted in the metadata for a given index and applies only to the duration of a current DDL statement. Therefore, the `RESUMABLE = ON` clause must be specified explicitly to enable resumability.
- `MAX_DURATION` option is supported for `RESUMABLE = ON` option or the `low_priority_lock_wait` option.
  - MAX_DURATION for RESUMABLE option specifies the time interval for an index being rebuild. Once this time is used the index rebuild is either paused or it completes its execution. User decides when a rebuild for a paused index can be resumed. The **time** (in minutes) for `MAX_DURATION` must be greater than 0 minutes and less or equal one week (7 \* 24 \* 60 = 10080 minutes). Having a long pause for an index operation may impact the DML performance on a specific table as well as the database disk capacity since both indexes the original one and the newly created one require disk space and need to be updated during DML operations. If `MAX_DURATION` option is omitted, the index operation will continue until its completion or until a failure occurs.
  - The `low_priority_lock_wait` argument option allows you to decide how the index operation can proceed when blocked on the Sch-M lock.

- Re-executing the original `ALTER INDEX REBUILD` statement with the same parameters resumes a paused index rebuild operation. You can also resume a paused index rebuild operation by executing the `ALTER INDEX RESUME` statement.
- The `SORT_IN_TEMPDB = ON` option isn't supported for resumable index
- The DDL command with `RESUMABLE = ON` can't be executed inside an explicit transaction (can't be part of `BEGIN TRAN ... COMMIT` block).
- Only index operations that are paused are resumable.
- When resuming an index operation that is paused, you can change the MAXDOP value to a new value. If MAXDOP isn't specified when resuming an  index operation that is paused, the last MAXDOP value is taken. IF the MAXDOP option isn't specified at all for index rebuild operation, the default value is taken.
- To pause immediately the index operation, you can stop the ongoing command (Ctrl-C) or you can execute the `ALTER INDEX PAUSE` command or the `KILL <session_id>` command. Once the command is paused it can be resumed using `RESUME` option.
- The `ABORT` command kills the session that hosted the original index rebuild and aborts the index operation
- No extra resources are required for resumable index rebuild except for
  - Additional space required to keep the index being built, including the time when index is being paused
  - A DDL state preventing any DDL modification
- The ghost cleanup will be running during the index pause phase, but it will be paused during index run.
The following functionality is disabled for resumable index rebuild operations
  - Rebuilding an index that is disabled isn't supported with `RESUMABLE = ON`
  - `ALTER INDEX REBUILD ALL` command
  - `ALTER TABLE` using index rebuild
  - DDL command with `RESUMABLE = ON` can't be executed inside an explicit transaction (can't be part of `BEGIN TRAN ... COMMIT` block)
  - Rebuild an index that has computed or TIMESTAMP column(s) as key columns.
- In case the base table contains LOB column(s) resumable clustered index rebuild requires a Sch-M lock in the Starting of this operation

> [!NOTE]  
> The DDL command runs until it completes, pauses or fails. In case the command pauses, an error will be issued indicating that the operation was paused and that the index creation did not complete. More information about the current index status can be obtained from [sys.index_resumable_operations](../../relational-databases/system-catalog-views/sys-index-resumable-operations.md). As before in case of a failure an error will be issued as well.

### <a id="wait-at-low-priority"></a> WAIT_AT_LOW_PRIORITY with online index operations

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

The `low_priority_lock_wait` syntax allows for specifying `WAIT_AT_LOW_PRIORITY` behavior. `WAIT_AT_LOW_PRIORITY` can be used with `ONLINE = ON` only.

In order to execute the DDL statement for an online index rebuild, all active blocking transactions running on a particular table must be completed. When the online index rebuild executes, it blocks all new transactions that are ready to start execution on this table. Although the duration of the lock for online index rebuild is very short, waiting for all open transactions on a given table to complete and blocking the new transactions to start, might significantly affect the throughput, causing a workload slow down or timeout, and significantly limit access to the underlying table.

The `WAIT_AT_LOW_PRIORITY` option allows DBAs to manage the Schema Stability (Sch-S) locks and Schema Modify (Sch-M) locks required for online index rebuilds and allows them to select one of two options. In either case, if during the wait time `MAX_DURATION = n [minutes]`, there are no blocking activities, the online index rebuild is executed immediately without waiting and the DDL statement is completed.

`WAIT_AT_LOW_PRIORITY` indicates that the online index rebuild operation will wait for low priority locks, allowing other operations to proceed while the online index build operation is waiting. Omitting the `WAIT AT LOW PRIORITY` option is equivalent to `WAIT_AT_LOW_PRIORITY (MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`.

MAX_DURATION = *time* [**MINUTES**]

The wait time (an integer value specified in minutes) that the online index rebuild locks will wait with low priority when executing the DDL command. If the operation is blocked for the `MAX_DURATION` time, the specified `ABORT_AFTER_WAIT` action will be executed. `MAX_DURATION` time is always in minutes, and the word **MINUTES** can be omitted.

ABORT_AFTER_WAIT = [ **NONE** | **SELF** | **BLOCKERS** ]

NONE  
Continue waiting for the lock with normal (regular) priority.

SELF  
Exit the online index rebuild DDL operation currently being executed without taking any action. The option **SELF** can't be used with a `MAX_DURATION` of 0.

BLOCKERS  
Kill all user transactions that block the online index rebuild DDL operation so that the operation can continue. The **BLOCKERS** option requires the login to have `ALTER ANY CONNECTION` permission.

## Spatial index restrictions

When you rebuild a spatial index, the underlying user table is unavailable during the index operation because the spatial index holds a schema lock.

The PRIMARY KEY constraint in the user table can't be modified while a spatial index is defined on a column of that table. To change the PRIMARY KEY constraint, first drop every spatial index of the table. After modifying the PRIMARY KEY constraint, you can re-create each of the spatial indexes.

In a single partition rebuild operation, you can't specify any spatial indexes. However, you can specify spatial indexes in a complete partition rebuild.

To change options that are specific to a spatial index, such as `BOUNDING_BOX` or `GRID`, you can either use a `CREATE SPATIAL INDEX` statement that specifies `DROP_EXISTING = ON`, or drop the spatial index and create a new one. For an example, see [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md).

## Data compression

For a more information about data compression, see [Data Compression](../../relational-databases/data-compression/data-compression.md).

To evaluate how changing PAGE and ROW compression will affect a table, an index, or a partition, use the [sp_estimate_data_compression_savings](../../relational-databases/system-stored-procedures/sp-estimate-data-compression-savings-transact-sql.md) stored procedure.

The following restrictions apply to partitioned indexes:

- When you use `ALTER INDEX ALL ...`, you can't change the compression setting of a single partition if the table has nonaligned indexes.
- The `ALTER INDEX <index> ... REBUILD PARTITION ...` syntax rebuilds the specified partition of the index.
- The `ALTER INDEX <index> ... REBUILD WITH ...` syntax rebuilds all partitions of the index.

## Statistics

When you execute `ALTER INDEX ALL ...` on a table, only the statistics associates with indexes are updated. Automatic or manual statistics created on the table (instead of an index) aren't updated.

## Permissions

To execute `ALTER INDEX`, at a minimum, `ALTER` permission on the table or view is required.

## Version Notes

- [!INCLUDE[ssSDS](../../includes/sssds-md.md)] doesn't use filegroup and filestream options.
- Columnstore indexes aren't available prior to [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)].
- Resumable index operations are available starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)].

## Basic syntax example

```sql
ALTER INDEX index1 ON table1 REBUILD;

ALTER INDEX ALL ON table1 REBUILD;

ALTER INDEX ALL ON dbo.table1 REBUILD;
```

## Examples: Columnstore Indexes

These examples apply to columnstore indexes.

### A. REORGANIZE demo

This example demonstrates how the `ALTER INDEX REORGANIZE` command works.  It creates a table that has multiple rowgroups, and then demonstrates how `REORGANIZE` merges the rowgroups.

```sql
-- Create a database
CREATE DATABASE [ columnstore ];
GO

-- Create a rowstore staging table
CREATE TABLE [ staging ] (
     AccountKey              int NOT NULL,
     AccountDescription      nvarchar (50),
     AccountType             nvarchar(50),
     AccountCodeAlternateKey     int
     )

-- Insert 10 million rows into the staging table.
DECLARE @loop int
DECLARE @AccountDescription varchar(50)
DECLARE @AccountKey int
DECLARE @AccountType varchar(50)
DECLARE @AccountCode int

SELECT @loop = 0
BEGIN TRAN
    WHILE (@loop < 300000)
      BEGIN
        SELECT @AccountKey = CAST (RAND()*10000000 as int);
        SELECT @AccountDescription = 'accountdesc ' + CONVERT(varchar(20), @AccountKey);
        SELECT @AccountType = 'AccountType ' + CONVERT(varchar(20), @AccountKey);
        SELECT @AccountCode =  CAST (RAND()*10000000 as int);

        INSERT INTO  staging VALUES (@AccountKey, @AccountDescription, @AccountType, @AccountCode);

        SELECT @loop = @loop + 1;
    END
COMMIT

-- Create a table for the clustered columnstore index

CREATE TABLE cci_target (
     AccountKey              int NOT NULL,
     AccountDescription      nvarchar (50),
     AccountType             nvarchar(50),
     AccountCodeAlternateKey int
     )

-- Convert the table to a clustered columnstore index named inxcci_cci_target;
CREATE CLUSTERED COLUMNSTORE INDEX idxcci_cci_target ON cci_target;
```

Use the TABLOCK option to insert rows in parallel. Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)], the `INSERT INTO` operation can run in parallel when TABLOCK is used.

```sql
INSERT INTO cci_target WITH (TABLOCK)
SELECT TOP 300000 * FROM staging;
```

Run this command to see the OPEN delta rowgroups. The number of rowgroups depends on the degree of parallelism.

```sql
SELECT *
FROM sys.dm_db_column_store_row_group_physical_stats
WHERE object_id  = object_id('cci_target');
```

Run this command to force all CLOSED and OPEN rowgroups into the columnstore.

```sql
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

Run this command again and you will see that smaller rowgroups are merged into one compressed rowgroup.

```sql
ALTER INDEX idxcci_cci_target ON cci_target REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

### B. Compress CLOSED delta rowgroups into the columnstore

This example uses the `REORGANIZE` option to compress each CLOSED delta rowgroup into the columnstore as a compressed  rowgroup. This isn't necessary, but is useful when the tuple-mover isn't compressing CLOSED rowgroups fast enough.

You can run both example in the [!INCLUDE [sssampledbdwobject-md](../../includes/sssampledbdwobject-md.md)] sample database.

This sample will run REORGANIZE on all partitions.

```sql
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;
```

This sample will run REORGANIZE on a specific partition.

```sql
-- REORGANIZE a specific partition
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0;
```

### C. Compress all OPEN AND CLOSED delta rowgroups into the columnstore

**Applies to:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

The command `REORGANIZE WITH ( COMPRESS_ALL_ROW_GROUPS = ON )` compresses each OPEN and CLOSED delta rowgroup into the columnstore as a compressed  rowgroup. This empties the deltastore and forces all rows to get compressed into the columnstore. This is useful especially after performing many insert operations since these operations store the rows in one or more delta rowgroups.

REORGANIZE combines rowgroups to fill rowgroups up to a maximum number of rows <= 1,024,576. Therefore, when you compress all OPEN and CLOSED rowgroups you won't end up with lots of compressed rowgroups that only have a few rows in them. You want rowgroups to be as full as possible to reduce the compressed size and improve query performance.

The following examples use the [!INCLUDE [sssampledbdwobject-md](../../includes/sssampledbdwobject-md.md)] database.

This example moves all OPEN and CLOSED delta rowgroups into the columnstore index.

```sql
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

This example moves all OPEN AND CLOSED delta rowgroups into the columnstore index for a specific partition.

```sql
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE PARTITION = 0 WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

### D. Defragment a columnstore index online

Doesn't apply to: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)].

Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)], REORGANIZE does more than compress delta rowgroups into the columnstore. It also performs online defragmentation. First, it reduces the size of the columnstore by physically removing deleted rows when 10% or more of the rows in a rowgroup have been deleted.  Then, it combines rowgroups together to form larger rowgroups that have up to the maximum of 1,024,576 rows per rowgroups.  All rowgroups that are changed get recompressed.

> [!NOTE]  
> Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)], rebuilding a columnstore index is no longer necessary in most situations since REORGANIZE physically removes deleted rows and merges rowgroups. The COMPRESS_ALL_ROW_GROUPS option forces all OPEN or CLOSED delta rowgroups into the columnstore which previously could only be done with a rebuild. REORGANIZE is online and occurs in the background so queries can continue as the operation happens.

The following example performs a REORGANIZE to defragment the index by physically removing rows that have been logically deleted from the table, and merging rowgroups.

```sql
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REORGANIZE;
```

### E. Rebuild a clustered columnstore index offline

Applies to: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])

> [!TIP]
> Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)] and in [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], we recommend using `ALTER INDEX REORGANIZE` instead of `ALTER INDEX REBUILD` for columnstore indexes.

> [!NOTE]  
> In [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] and [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], `REORGANIZE` is only used to compress CLOSED rowgroups into the columnstore. The only way to perform defragmentation operations and to force all delta rowgroups into the columnstore is to rebuild the index.

This example shows how to rebuild a clustered columnstore index and force all delta rowgroups into the columnstore. This first step prepares a table `FactInternetSales2` in the [!INCLUDE [sssampledbdwobject-md](../../includes/sssampledbdwobject-md.md)] database with a clustered columnstore index, and inserts data from the first four columns.

```sql
CREATE TABLE dbo.FactInternetSales2 (
    ProductKey [int] NOT NULL,
    OrderDateKey [int] NOT NULL,
    DueDateKey [int] NOT NULL,
    ShipDateKey [int] NOT NULL);

CREATE CLUSTERED COLUMNSTORE INDEX cci_FactInternetSales2
ON dbo.FactInternetSales2;

INSERT INTO dbo.FactInternetSales2
SELECT ProductKey, OrderDateKey, DueDateKey, ShipDateKey
FROM dbo.FactInternetSales;

SELECT * FROM sys.column_store_row_groups;
```

The results show one OPEN rowgroup, which means [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] will wait for more rows to be added before it closes the rowgroup and moves the data to the columnstore. This next statement rebuilds the clustered columnstore index, which forces all rows into the columnstore.

```sql
ALTER INDEX cci_FactInternetSales2 ON FactInternetSales2 REBUILD;
SELECT * FROM sys.column_store_row_groups;
```

The results of the `SELECT` statement show the rowgroup is COMPRESSED, which means the column segments of the rowgroup are now compressed and stored in the columnstore.

### F. Rebuild a partition of a clustered columnstore index offline

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)])

To rebuild a partition of a large clustered columnstore index, use `ALTER INDEX REBUILD` with the partition option. This example rebuilds partition 12. Starting with [!INCLUDE[sssql16-md](../../includes/sssql16-md.md)], we recommend replacing `REBUILD` with `REORGANIZE`.

```sql
ALTER INDEX cci_fact3
ON fact3
REBUILD PARTITION = 12;
```

### G. Change a clustered columnstore index to use archival compression

Doesn't apply to: [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]

You can choose to reduce the size of a clustered columnstore index even further by using the COLUMNSTORE_ARCHIVE data compression option. This is practical for older data that you want to keep on cheaper storage. We recommend only using this on data that isn't accessed often since decompress is slower than with the normal COLUMNSTORE compression.

The following example rebuilds a clustered columnstore index to use archival compression, and then shows how to remove the archival compression. The final result will use only columnstore compression.

First, prepare the example by creating a table with a clustered columnstore index. Then, compress the table further by using archival compression.

```sql
--Prepare the example by creating a table with a clustered columnstore index.
CREATE TABLE SimpleTable (
    ProductKey [int] NOT NULL,
    OrderDateKey [int] NOT NULL,
    DueDateKey [int] NOT NULL,
    ShipDateKey [int] NOT NULL
);

CREATE CLUSTERED INDEX cci_SimpleTable ON SimpleTable (ProductKey);

CREATE CLUSTERED COLUMNSTORE INDEX cci_SimpleTable
ON SimpleTable
WITH (DROP_EXISTING = ON);

--Compress the table further by using archival compression.
ALTER INDEX cci_SimpleTable ON SimpleTable
REBUILD
WITH (DATA_COMPRESSION = COLUMNSTORE_ARCHIVE);
GO
```

This sample removes the archive compression, and only uses columnstore compression.

```sql
ALTER INDEX cci_SimpleTable ON SimpleTable
REBUILD
WITH (DATA_COMPRESSION = COLUMNSTORE);
GO
```

## Examples: Rowstore indexes

### A. Rebuild an index

The following example rebuilds a single index on the `Employee` table in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database.

```sql
ALTER INDEX PK_Employee_EmployeeID ON HumanResources.Employee REBUILD;
```

### B. Rebuild all indexes on a table and specify options

The following example specifies the keyword ALL. This rebuilds all indexes associated with the table `Production.Product` in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database. Three options are specified.

```sql
ALTER INDEX ALL ON Production.Product
REBUILD WITH (FILLFACTOR = 80, SORT_IN_TEMPDB = ON, STATISTICS_NORECOMPUTE = ON);
```

The following example adds the ONLINE option including the low priority lock option, and adds the row compression option.

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

```sql
ALTER INDEX ALL ON Production.Product
REBUILD WITH
(
    FILLFACTOR = 80,
    SORT_IN_TEMPDB = ON,
    STATISTICS_NORECOMPUTE = ON,
    ONLINE = ON ( WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 4 MINUTES, ABORT_AFTER_WAIT = BLOCKERS ) ),
    DATA_COMPRESSION = ROW
);
```

### C. Reorganize an index with LOB compaction

The following example reorganizes a single clustered index in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database. Because the index contains a LOB data type in the leaf level, the statement also compacts all pages that contain the large object data. Specifying the `WITH (LOB_COMPACTION = ON)` option isn't required because the default value is ON.

```sql
ALTER INDEX PK_ProductPhoto_ProductPhotoID ON Production.ProductPhoto REORGANIZE WITH (LOB_COMPACTION = ON);
```

### D. Set options on an index

The following example sets several options on the index `AK_SalesOrderHeader_SalesOrderNumber` in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database.

```sql
ALTER INDEX AK_SalesOrderHeader_SalesOrderNumber ON
    Sales.SalesOrderHeader
SET (
    STATISTICS_NORECOMPUTE = ON,
    IGNORE_DUP_KEY = ON,
    ALLOW_PAGE_LOCKS = ON
    ) ;
GO
```

### E. Disable an index

The following example disables a nonclustered index on the `Employee` table in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database.

```sql
ALTER INDEX IX_Employee_ManagerID ON HumanResources.Employee DISABLE;
```

### F. Disable constraints

The following example disables a PRIMARY KEY constraint by disabling the PRIMARY KEY index in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database. The FOREIGN KEY constraint on the underlying table is automatically disabled and warning message is displayed.

```sql
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department DISABLE;
```

The result set returns this warning message.

```output
Warning: Foreign key 'FK_EmployeeDepartmentHistory_Department_DepartmentID'
on table 'EmployeeDepartmentHistory' referencing table 'Department'
was disabled as a result of disabling the index 'PK_Department_DepartmentID'.
```

### G. Enable constraints

The following example enables the PRIMARY KEY and FOREIGN KEY constraints that were disabled in Example F.

The PRIMARY KEY constraint is enabled by rebuilding the PRIMARY KEY index.

```sql
ALTER INDEX PK_Department_DepartmentID ON HumanResources.Department REBUILD;
```

The FOREIGN KEY constraint is then enabled.

```sql
ALTER TABLE HumanResources.EmployeeDepartmentHistory
CHECK CONSTRAINT FK_EmployeeDepartmentHistory_Department_DepartmentID;
GO
```

### H. Rebuild a partitioned index

The following example rebuilds a single partition, partition number `5`, of the partitioned index `IX_TransactionHistory_TransactionDate` in the [!INCLUDE [sssampledbobject-md](../../includes/sssampledbobject-md.md)] database. Partition 5 is rebuilt with `ONLINE=ON` and the 10 minutes wait time for the low priority lock applies separately to every lock acquired by index rebuild operation. If during this time the lock can't be obtained to complete index rebuild, the rebuild operation statement itself is aborted, due to `ABORT_AFTER_WAIT = SELF`.

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

```sql
-- Verify the partitioned indexes.
SELECT *
FROM sys.dm_db_index_physical_stats (DB_ID(),OBJECT_ID(N'Production.TransactionHistory'), NULL , NULL, NULL);
GO
--Rebuild only partition 5.
ALTER INDEX IX_TransactionHistory_TransactionDate
ON Production.TransactionHistory
REBUILD Partition = 5
   WITH (ONLINE = ON (WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10 minutes, ABORT_AFTER_WAIT = SELF)));
GO
```

### I. Change the compression setting of an index

The following example rebuilds an index on a nonpartitioned rowstore table.

```sql
ALTER INDEX IX_INDEX1
ON T1
REBUILD
WITH (DATA_COMPRESSION = PAGE);
GO
```

### J. Change the setting of an index with XML compression

**Applies to**: [!INCLUDE[sssql22-md](../../includes/sssql22-md.md)] and later versions, [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)], and [!INCLUDE [ssazuremi](../../includes/ssazuremi_md.md)].

The following example rebuilds an index on a nonpartitioned rowstore table.

```sql
ALTER INDEX IX_INDEX1
ON T1
REBUILD
WITH (XML_COMPRESSION = ON);
GO
```

For more data compression examples, see [Data Compression](../../relational-databases/data-compression/data-compression.md).

### K. Online resumable index rebuild

**Applies to**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (Starting with [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)]) and [!INCLUDE [ssazure-sqldb](../../includes/ssazure-sqldb.md)]

The following examples show how to use online resumable index rebuild.

1. Execute an online index rebuild as resumable operation with MAXDOP = 1.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE = ON, MAXDOP = 1, RESUMABLE = ON) ;
   ```

2. Executing the same command again (see above) after an index operation was paused, resumes automatically the index rebuild operation.

3. Execute an online index rebuild as resumable operation with MAX_DURATION set to 240 minutes.

   ```sql
   ALTER INDEX test_idx on test_table REBUILD WITH (ONLINE = ON, RESUMABLE = ON, MAX_DURATION = 240) ;
   ```

4. Pause a running resumable online index rebuild.

   ```sql
   ALTER INDEX test_idx on test_table PAUSE ;
   ```

5. Resume an online index rebuild for an index rebuild that was executed as resumable operation specifying a new value for MAXDOP set to 4.

   ```sql
   ALTER INDEX test_idx on test_table RESUME WITH (MAXDOP = 4) ;
   ```

6. Resume an online index rebuild operation for an index online rebuild that was executed as resumable. Set MAXDOP to 2, set the execution time for the index being running as resumable to 240 minutes, and if an index is being blocked on the lock, wait 10 minutes and after that kill all blockers.

   ```sql
      ALTER INDEX test_idx on test_table
         RESUME WITH (MAXDOP = 2, MAX_DURATION = 240 MINUTES,
         WAIT_AT_LOW_PRIORITY (MAX_DURATION = 10, ABORT_AFTER_WAIT = BLOCKERS)) ;
   ```

7. Abort resumable index rebuild operation which is running or paused.

   ```sql
   ALTER INDEX test_idx on test_table ABORT ;
   ```

## See also

- [SQL Server Index Architecture and Design Guide](../../relational-databases/sql-server-index-design-guide.md)
- [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md)
- [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)
- [CREATE SPATIAL INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-spatial-index-transact-sql.md)
- [CREATE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-xml-index-transact-sql.md)
- [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)
- [Disable Indexes and Constraints](../../relational-databases/indexes/disable-indexes-and-constraints.md)
- [XML Indexes &#40;SQL Server&#41;](../../relational-databases/xml/xml-indexes-sql-server.md)
- [Reorganize and Rebuild Indexes](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)
- [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)
- [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)
